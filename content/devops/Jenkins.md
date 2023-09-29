---
title: Jenkins
parent: DevOps
---

# Jenkins
{: .no_toc }

## Inhalt
{: .no_toc }
- TOC
{:toc}

## Pipeline

### Declarative

#### Sections

##### Steps
- <https://www.jenkins.io/doc/pipeline/steps/workflow-basic-steps/>
- **checkout**
```groovy
checkout([
	$class: 'GitSCM',
	branches: [[name: '*/master']],
	extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'somedir']],
	userRemoteConfigs: [[credentialsId: 'cred-id', url: 'https://some.repo.git']]
])
```
- **echo**
	- `echo "message"`
- **sh**
```groovy
def collectStderr(String script) {
  return sh(returnStdout: true, script: "${script} 2>&1") // 1 = stdout, 2 = stderr
}
```

#### Directives
- <https://www.jenkins.io/doc/book/pipeline/syntax/#declarative-directives>

##### Options
- <https://www.jenkins.io/doc/book/pipeline/syntax/#options>
- **timeout**
	- `timeout(time: 20, unit: 'SECONDS', activity: true) { ... }`

##### Parameters
- <https://www.jenkins.io/doc/book/pipeline/syntax/#parameters>
```groovy
pipeline {
	parameters {
		booleanParam(name: 'foo', defaultValue: false, description: 'bar'),
		choiceParam(name: 'bar', choices: ['qux', 'quux'], description: '')
	}
}
```

#### Beispiel
```groovy
def sayHello(to) {
    println('hello ' + to) 
}

pipeline {
    agent any
    parameters {
        booleanParam(name: 'bool', defaultValue: false, description: 'yes?')
    }
    options {
        buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '10', daysToKeepStr: '', numToKeepStr: '10'))
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES', activity: true)
        skipDefaultCheckout()
    }
    tools {
        jdk 'openjdk-11'
	maven 'maven-3.6.3'
    }
    stages {
    	 stage('checkout') {
 	     steps {
	         checkout scm
	     }
	 }
	 stage('library') {
	 	steps {
	                library identifier: 'my-lib@<git-tag>', retriever: modernSCM([
	                    $class: 'GitSCMSource',
	                    remote: 'https://my.git/shared-library.git',
	                    credentialsId: '<credentials-id>'
	                ])
	                script {
	                    String resource = libraryResource 'foo/bar/example.txt' // resources/foo/bar/example.txt
	                    writeFile file: 'foo.txt', text: resource
	                }
		}
	 }
         stage('1') {
	     steps {
	         sayHello('world')
		 sh "mvn --batch-mode --no-transfer-progress clean package -DskipTests=false"
		 sh """
		     docker run -p 8080:8080 \
		     --env FOO=bar \
		     some-image
		 """
	     }
	 }
	 stage('parallel') {
	     parallel {
	          stage('A') {
	   		steps {
		      		echo "A"
	  		}
		  }
		  stage('B') {
    			steps {
		      		echo "B"
	  		}
		  }
	     }
	 }
  	stage('agent') {
   		agent {
     			docker {
				reuseNode true
                    		image 'ghcr.io/graalvm/jdk:ol8-java17-22.3.1'
                    		args '-e FOO=BAR -e BAZ=QUX'
			}
     		}
       		steps {
	 		sh 'java -version'
	 	}
   	}
    }
}
```

### Scripted

#### Parameters
```groovy
properties([
	parameters([
		booleanParam(name: 'foo', defaultValue: false, description: 'bar'),
		choiceParam(name: 'bar', choices: ['qux', 'quux'], description: '')
	])
])
node { ... }
```

#### Parallel
```
parallel([
	'failFast': true,
	'foo': { echo "foo" },
	'bar': { echo "bar" }
])
```

#### Triggers
**upstream**
```groovy
pipelineTriggers([
     upstream(threshold: 'SUCCESS', upstreamProjects: './foo')
])
```

**scheduled**
```groovy
pipelineTriggers([
  cron('H 23 * * *')
])
// also supports predefined aliases
// @hourly (0 * * * *)
// @daily/@midnight (0 0 * * *)
// @weekly (0 0 * * 0; sunday morning)
// @monthly (0 0 1 * *; midnight of first day of month)
```

#### Beispiel
```groovy
// scripted
properties([
	parameters([
        	booleanParam(name: 'CLEAN_WS', defaultValue: false, description: 'Workspace vorher löschen?'),
		choice(
		    name: 'BAR',
		    choices: [
			'lorem'
			'ipsum',
			'dolor'
		    ],
		    description: 'bar'
		),
		string(name: 'BAZ', defaultValue: '2.3.0-SNAPSHOT', description: '')
	]),
  	[$class: 'BuildDiscarderProperty', strategy: [$class: 'LogRotator', artifactDaysToKeepStr: '', artifactNumToKeepStr: '10', daysToKeepStr: '', numToKeepStr: '10']],
	[$class: 'DurabilityHintJobProperty', hint: 'PERFORMANCE_OPTIMIZED']
])

node {
  	currentBuild.description = "${params}"
	stage('Clean WS') {
		if (!params.CLEAN_WS) {
			catchError(message: "Stage 'Clean WS' übersprungen", buildResult: "SUCCESS", stageResult: "UNSTABLE") {
				sh "exit 1"
			}
			return;
		}
		cleanWs()
	}
	stage('Checkout') {
		checkout scm
	}
  	stage('foo.sh') {
		timeout(time: 10, unit: 'SECONDS') {
			sh "chmod 755 ${env.WORKSPACE}/foo.sh"
			retry(2) {
				sh "${env.WORKSPACE}/foo.sh"
			}

		}
  	}
   	stage('X') {
	    	if (skip) {
      			// Stage überspringen, als UNSTABLE markieren
	    		catchError(message: "Stage 'foo' übersprungen", stageResult: 'UNSTABLE', buildResult: 'SUCCESS') {
	     			sh "exit 1"
			}
	    		return
	  	}

		def cause = currentBuild.getBuildCauses('jenkins.branch.BranchIndexingCause')

		boolean buildCausedByBranchIndexing = !new java.util.ArrayList<Object>(cause).isEmpty()
		if (buildCausedByBranchIndexing) {
			echo "Build durch Branch-Indexing ausgelöst => abbrechen"
			currentBuild.result = 'ABORTED'
			return
		}

		cause = currentBuild.getBuildCauses('hudson.model.Cause$UserIdCause')
		if (cause) {
			print(cause.getClass()) // class net.sf.json.JSONArray
			print("${cause[0].userId") // fbar
			print("${cause[0].userName") // Foo Bar
			print("${cause[0].shortDescription") // Started by user Foo Bar
		}

		def javaHome = tool name: 'openjdk-8'
		def mvnHome = tool name: 'maven-3.6.3'
		withEnv(["PATH=${javaHome}/bin:${mvnHome}/bin:$PATH", "JAVA_HOME=${javaHome}"]) {
		    sh "java -version"
		    sh "mvn -version"
		}
    	}
}

def pseudoBreakpoint() {
    def i
    try {
        i = input(
            message: 'Enter sh script',
            ok: 'Execute',
            parameters: [
                string(defaultValue: '', description: 'Abort to continue pipeline execution', name: 'script', trim: true)
            ]
        )
    } catch (e) { // Caused by 'Abort'
        return
    }
    try {
        sh(i)
    } catch (e) {
        println('sh script error: ' + e.getMessage())
    }
    pseudoBreakpoint()
}
```


### Globals
- <https://opensource.triology.de/jenkins/pipeline-syntax/globals>
- siehe Link Hinweis unten; nur die wenigsten sind writable. Umgehen ggf. mit `currentBuild.rawBuild.@foo = bar`
- **currentBuild**
	- description
	- result
	- <https://opensource.triology.de/jenkins/pipeline-syntax/globals#currentBuild>
- **params**
	- `${params.FOO}` 
- **env**
	- WORKSPACE
		- `${env.WORKSPACE}`
		- absoluter Pfad des Workspace, z. B. /var/jenkins_home/workspace/foo
- **pipeline**
- **scm**


## Groovy
```groovy
// a.groovy
def call(Closure c) {
  println('foo')
  c()
}

// z.groovy
a {
  println('bar')
}


// b.groovy
def func1() { ... }
def func2() { ... }

// z.groovy
b.func1()
b.func2()


// c.groovy
def call(body) {
    def config = [:]
    body.resolveStrategy = Closure.DELEGATE_FIRST
    body.delegate = config
    body()
    println('hello ' + config.name)
}

// z.groovy
c {
  name = 'world'
}


// d.groovy
def call(String name, Closure c) {
  println('hello ' + name)
  c()
}

// z.groovy
d('world') {
  println('foo')
}

// left shift mutiert Map
def map = [foo: 'foo', bar: 'bar']
map << [foo: null, baz: 'baz']
println(map) // { foo: null, bar: 'bar', baz: 'baz' }
```

### Whitespace
```groovy
def str = """
foo
 bar
"""
println(str)
//foo
// bar

def str = """
	  foo
	   bar
	  """
println(str)
//                             foo
//                              bar

def str = """\
	  foo
	   bar
	  """
println(str)
//                             foo
//                              bar

def str = """\
	  foo
	   bar
	  """.stripIndent()
println(str)
//foo
// bar

def str = """\
	  foo
	  bar
	  """.stripIndent().replace('\n', ' ')
println(str)
//foo bar

def str = """\
	  	foo
	  	bar
	  """.stripIndent().replace('\n', ' ')
println(str)
//foo bar
```

## Plugins
- **docker**
  - <https://docs.cloudbees.com/docs/admin-resources/latest/plugins/docker-workflow>
  - File aus Container zum Host kopieren:
    ```groovy
    def image = ...
    image.withRun { container ->
      sh "docker cp ${container.id}:/path/in/container/file.txt /path/in/host/file.txt" 
    }
    ```
- **configuration-as-code**
  - <https://github.com/jenkinsci/configuration-as-code-plugin>
- **Timestamper**
	- oder: timestamps-Option (<https://www.jenkins.io/doc/book/pipeline/syntax/#available-options>) 
	- *adds timestamps to the console output of Jenkins jobs*
	- <https://plugins.jenkins.io/timestamper/>
- **Config File Provider**
	- <https://plugins.jenkins.io/config-file-provider/>
- **Active Choices**
	- *create scripted, dynamic and interactive job parameters*
	- 3 neue Parametertypen
		- Active Choice
			- gerendered als Checkboxen, Radio-Buttons oder Dropdown
			- ```groovy
				properties([
					parameters([
						// ChoiceParameter; <https://github.com/jenkinsci/active-choices-plugin/blob/master/src/main/java/org/biouno/unochoice/ChoiceParameter.java>
						[
							$class: 'ChoiceParameter',
							choiceType: 'PT_SINGLE_SELECT', // <https://github.com/jenkinsci/active-choices-plugin/blob/master/src/main/java/org/biouno/unochoice/AbstractUnoChoiceParameter.java>
							description: 'Choose stage',
							// filterLength: 1,
							// filterable: true,
							name: 'Stage',
							// randomName: 'choice-parameter-5631314439613978',
							script: [
								// oder ScripterScript
								$class: 'GroovyScript', // <https://github.com/jenkinsci/active-choices-plugin/blob/master/src/main/java/org/biouno/unochoice/model/GroovyScript.java>
								fallbackScript: [
									classpath: [],
									sandbox: true,
									script: 'return [\"Error in stage script\"]'
								],
								script: [
									classpath: [],
									sandbox: true,
									script: 'return ["Dev", "QA", "Prod"]'
								]
							]
						]
						// CascadeChoiceParameter; <https://github.com/jenkinsci/active-choices-plugin/blob/master/src/main/java/org/biouno/unochoice/CascadeChoiceParameter.java>
						// DynamicReferenceParameter; <https://github.com/jenkinsci/active-choices-plugin/blob/master/src/main/java/org/biouno/unochoice/DynamicReferenceParameter.java>
					])
				])

				pipeline {
					agent any
					parameters {
						choice(name: 'STATIC_PARAM', choices: ['static_1', 'static_2'])
					}
					stages {
						stage('test') {
							steps {
								echo params.Stage
							}
						}
					}
				}
			  ```
		- Active Choice Reactive
			- reagiert auf Änderung eines anderen Parameters
			- gerendered wie Active Choice, zusätzlich mit Filter-Inputfeld
		- Active Choice Reactive Reference
			- reagiert auf Änderung eines anderen Parameters
			- gerendered als Liste, Input-Box oder beliebiges HTML 
	- <https://plugins.jenkins.io/uno-choice/>


## Tools
- **jenkinsfile-runner**
  - <https://github.com/jenkinsci/jenkinsfile-runner>
  - *packages Jenkins pipeline execution engine as a command line tool or as a Docker image*
- **vscode-groovy-lint** → IDE/VSCode


## Docker
```
FROM jenkinsci/blueocean:latest
USER root
RUN apk update && apk upgrade && apk add maven git nodejs npm
USER jenkins
```

## Shared Library
- <https://github.com/Diabol/jenkins-pipeline-shared-library-template>
- <https://stackoverflow.com/questions/47205761/how-can-i-define-a-global-variable-or-constant-using-jenkins-pipeline-shared-lib>
