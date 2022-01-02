---
tags: [Notebooks/DevOps]
title: Jenkins
created: '2020-07-09T09:11:44.636Z'
modified: '2021-07-21T11:42:44.818Z'
parent: DevOps
---

# Jenkins

- [globale Variablen](https://opensource.triology.de/jenkins/pipeline-syntax/globals)
  - [currentBuild](https://opensource.triology.de/jenkins/pipeline-syntax/globals#currentBuild)
    - siehe Link Hinweis unten; nur die wenigsten sind writable. Umgehen ggf. mit `currentBuild.rawBuild.@foo = bar`


## Jenkinsfile

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
