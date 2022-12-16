---
tags: [Notebooks/DevOps]
title: Jenkins
created: '2020-07-09T09:11:44.636Z'
modified: '2021-07-21T11:42:44.818Z'
parent: DevOps
---

# Jenkins

## Steps
- <https://www.jenkins.io/doc/pipeline/steps/workflow-basic-steps/>
- **echo**
	- `echo "message"` 
- **properties**
- **sh**
- **checkout**
- **timeout**
  - `timeout(time: 20, unit: 'SECONDS', activity: true) { ... }`
  - <https://www.jenkins.io/doc/pipeline/steps/workflow-basic-steps/#timeout-enforce-time-limit>
- **parallel**
	- ```
	  parallel([
	    'failFast': true,
	    'foo': { echo "foo" },
	    'bar': { echo "bar" }
	  ])
	  ``` 
- **retry**
- **stage**
- **sleep**
- **input**
	- properties
		- message
		- parameters?
		- ...  
	- <https://www.jenkins.io/doc/pipeline/steps/pipeline-input-step/> 
- ...


## Symbols
- **node**
- **parameters**
- **cleanWs**
- **pipelineTriggers**
- **disableConcurrentBuilds**
- ...


## Globals
- <https://opensource.triology.de/jenkins/pipeline-syntax/globals>
- siehe Link Hinweis unten; nur die wenigsten sind writable. Umgehen ggf. mit `currentBuild.rawBuild.@foo = bar`
- **currentBuild**
	- description
	- result
	- <https://opensource.triology.de/jenkins/pipeline-syntax/globals#currentBuild>
- **params**
- **env**
	- WORKSPACE
		- `${env.WORKSPACE}`
		- absoluter Pfad des Workspace, z. B. /var/jenkins_home/workspace/foo
- **pipeline**
- **scm**


## Jenkinsfile

**Beispiele**
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
}
```

```groovy
// declarative
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
		      echo "A"
		  }
		  stage('B') {
		      echo "B"
		  }
	     }
	 }
    }
}
```

**Groovy**
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
```

**stderr**
<br/>
1 = stdout, 2 = stderr
```groovy
def collectStderr(String script) {
  return sh(returnStdout: true, script: "${script} 2>&1")
}
```

**upstream job trigger**
```groovy
pipelineTriggers([
     upstream(
         threshold: 'SUCCESS',
         upstreamProjects: './foo'
     )
])
```

**scheduled trigger**
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

**build cause**
```groovy
def buildCausedByUser = !new java.util.ArrayList<Object>(
    currentBuild.getBuildCauses('hudson.model.Cause$UserIdCause')
).isEmpty()
```
Branch Indexing löst alle Builds einer Multibranch-Pipeline aus:
Es gibt ein Property "Suppress Automatic SCM trigger" mit dem das verhindert werden kann, allerdings schaltet das auch eventuell vorhandene Commit-Trigger aus.
Daher:
```groovy
node {
	boolean buildCausedByBranchIndexing = !new java.util.ArrayList<Object>(
	    currentBuild.getBuildCauses('jenkins.branch.BranchIndexingCause')
	).isEmpty()
	if (buildCausedByBranchIndexing) {
		echo "Build durch Branch-Indexing ausgelöst => abbrechen"
		currentBuild.result = 'ABORTED'
		return
	}
```

**pseudo breakpoint**
```groovy
def call() {
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
    breakpoint()
}
```
oder <http://notes.asaleh.net/posts/debugging-jenkins-pipeline>

**stage überspringen, als UNSTABLE markieren**
```groovy
stage('foo') {
  if (skip) {
    catchError(message: "Stage 'foo' übersprungen", stageResult: 'UNSTABLE', buildResult: 'SUCCESS') {
      sh "exit 1"
    }
    return
  }
}
```

**PATH (scripted)**
```groovy
def javaHome = tool name: 'openjdk-8'
def mvnHome = tool name: 'maven-3.6.3'
withEnv(["PATH=${javaHome}/bin:${mvnHome}/bin:$PATH", "JAVA_HOME=${javaHome}"]) {
    sh "java -version"
    sh "mvn -version"
}
```

### properties

**parameters**
- boolean
  ```groovy
  properties([
    parameters([
      booleanParam(name: 'foo', defaultValue: false, description: 'bar')
    ])
  ])

  node { ... }
  ```


## Plugins
- docker
  - <https://docs.cloudbees.com/docs/admin-resources/latest/plugins/docker-workflow>
  - File aus Container zum Host kopieren:
    ```groovy
    def image = ...
    image.withRun { container ->
      sh "docker cp ${container.id}:/path/in/container/file.txt /path/in/host/file.txt" 
    }
    ```
- configuration-as-code
  - <https://github.com/jenkinsci/configuration-as-code-plugin>
- Timestamper
	- *adds timestamps to the console output of Jenkins jobs*
	- <https://plugins.jenkins.io/timestamper/> 


## Tools
- jenkinsfile-runner
  - <https://github.com/jenkinsci/jenkinsfile-runner>
  - *packages Jenkins pipeline execution engine as a command line tool or as a Docker image*
- vscode-groovy-lint → IDE/VSCode


## Docker
```
FROM jenkinsci/blueocean:latest
USER root
RUN apk update && apk upgrade && apk add maven git nodejs npm
USER jenkins
```
