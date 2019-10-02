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
    
  }
}