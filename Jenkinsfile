pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'hello devops playground'
        sh 'mvn clean install -Dlicense.skip=true'
      }
    }
  }
  tools {
    maven 'maven'
  }
}