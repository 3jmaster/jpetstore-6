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
      parallel {
        stage('test') {
          steps {
            sh 'mvn sonar:sonar -Dsonar.host.url=http://13.228.71.229:8081 -Dlicense.skip=true'
          }
        }
        stage('tester credentials') {
          steps {
            echo "The tester is ${TESTER}"
          }
        }
        stage('print build number') {
          steps {
            echo "This is build number ${BUILD_ID}"
          }
        }
        stage('double quotes') {
          steps {
            echo '"double quotes here"'
          }
        }
      }
    }
  }
  tools {
    maven 'maven'
  }
  environment {
    TESTER = 'fab'
  }
}