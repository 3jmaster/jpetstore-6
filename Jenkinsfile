pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'hello devops playground'
        sh 'mvn clean install -Dlicense.skip=true'
      }
    }
    stage('test') {
      steps {
        sh 'mvn sonar:sonar -Dsonar.host.url=http://13.228.71.229:8081 -Dlicense.skip=true'
      }
    }
  }
  tools {
    maven 'maven'
  }
}