# Getting started with Pipeline
Jenkins Pipeline (or simply "Pipeline" with a capital "P") is a suite of plugins which supports implementing and integrating continuous delivery pipelines into Jenkins.

A continuous delivery (CD) pipeline is an automated
expression of your process for getting software from version
control right through to your users and customers.

# Pipeline
A Pipeline is a user-defined model of a CD pipeline. A Pipeline’s code defines your entire build process, which typically includes stages for building an application, testing it and then delivering it.

### Node
A node is a machine which is part of the Jenkins environment and is capable of executing a Pipeline.

### Stage
A stage block defines a conceptually distinct subset of tasks performed through the entire Pipeline (e.g. "Build", "Test" and "Deploy" stages), which is used by many plugins to visualize or present Jenkins Pipeline status/progress. 

### Step
A single task. Fundamentally, a step tells Jenkins what to do at a particular point in time (or "step" in the process). For example, to execute the shell command ```sh make ``` use the sh step: sh ```sh 'make' ```. When a plugin extends the Pipeline DSL, [1] that typically means the plugin has implemented a new step.


# Defining a Pipeline
1. Declarative  
2. Scripted

Both Declarative and Scripted Pipeline are DSLs to describe portions of your software delivery pipeline. Scripted Pipeline is written in a limited form of Groovy syntax.

Jenkins job DSL is a plugin that allows us to define jobs in programmatic form with minimal effort.
DSL stands for Domain Specific Language.

- Jenkins job DSL plugin was designed to make it easier to manage jobs.
  - If you don’t have a lot of jobs, using the UI is the easiest way.
  - When the number of jobs grows, maintaining becomes difficult and a lot of work.

- Jenkins job DSL plugin solve this problem and you get a lot of extra benefits.

1. Declarative Pipeline fundamentals
  In Declarative Pipeline syntax, the pipeline block defines all the work done throughout your entire Pipeline.
  
  ```sh
  Jenkinsfile (Declarative Pipeline)
pipeline {
    agent any -> 1.
    stages {
        stage('Build') {  -> 2.
            steps {
                //  -> 3.
            }
        }
        stage('Test') {  -> 4.
            steps {
                //  -> 5.
            }
        }
        stage('Deploy') {  -> 6.
            steps {
                //  -> 7.
            }
        }
    }
}
```
1. Execute this Pipeline or any of its stages, on any available agent.
2. Defines the "Build" stage.
3. Perform some steps related to the "Build" stage.
4. Defines the "Test" stage.
5. Perform some steps related to the "Test" stage.
6. Defines the "Deploy" stage.
7. Perform some steps related to the "Deploy" stage.


# Scripted Pipeline fundamentals
In Scripted Pipeline syntax, one or more node blocks do the core work throughout the entire Pipeline. Although this is not a mandatory requirement of Scripted Pipeline syntax, confining your Pipeline’s work inside of a node block does two things:

1. Schedules the steps contained within the block to run by adding an item to the Jenkins queue. As soon as an executor is free on a node, the steps will run.
2. Creates a workspace (a directory specific to that particular Pipeline) where work can be done on files checked out from source control.

```sh 
Jenkinsfile (Scripted Pipeline)
node {   -> 1.
    stage('Build') {  -> 2.
        //  -> 3.
    }
    stage('Test') {  -> 4. 
        //  -> 5.
    }
    stage('Deploy') {  -> 6.
        //  -> 7.
    }
}
```
1. Execute this Pipeline or any of its stages, on any available agent.
2. Defines the "Build" stage. stage blocks are optional in Scripted Pipeline syntax. However, implementing stage blocks in a Scripted Pipeline provides clearer visualization of each stage’s subset of tasks/steps in the Jenkins UI.
3. Perform some steps related to the "Build" stage.
4. Defines the "Test" stage.
5. Perform some steps related to the "Test" stage.
6. Defines the "Deploy" stage.
7. Perform some steps related to the "Deploy" stage.

# Pipeline example

```sh 
pipeline {
  agent any

  stages {
    stage('Unit Tests') {
      steps {
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
      }
    }
    stage('build') {
      steps {
        sh 'ant -f build.xml -v'
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
    }
  }
}
```

