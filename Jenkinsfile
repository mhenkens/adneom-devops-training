pipeline {
  agent any
  environment {
      registry = "ffurlanetto"
      registryCredential = 'dockerhub'
    }
  options {
    timeout(10)
  }
  stages {
    stage('Build') {
     agent{
       label 'openjdk-11'
     }
      steps {
        sh './gradlew build'
        stash(allowEmpty: true, name: 'post-build')
      }
    }
    stage('Docker') {
      agent{
        label 'docker'
      }
      steps {
        unstash: 'post-buid'
        dir(path: 'asgard-rest') {
          script{
            docker.build(registry + "/asgard-rest:latest")
          }
        }

        dir(path: 'asgard-web') {
          script {
            docker.build(registry + "/asgard-web:latest")
          }
        }
      }
    }
  }
}