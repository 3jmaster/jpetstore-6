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
    stage('JFrog push') {
      steps {
        script {
          def server = Artifactory.server "artifactory"
          def buildInfo = Artifactory.newBuildInfo()
          def rtMaven = Artifactory.newMavenBuild()

          rtMaven.tool = 'maven'
          rtMaven.deployer server: server, releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local'

          buildInfo = rtMaven.run pom: 'pom.xml', goals: "clean install -Dlicense.skip=true"
          buildInfo.env.capture = true
          buildInfo.name = 'jpetstore-6'
          server.publishBuildInfo buildInfo
        }

      }
    }
    stage('Deploy prompt') {
      steps {
        input 'Deploy to Production?'
      }
    }
    stage('Deployment') {
      steps {
        echo '"Print message"'
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