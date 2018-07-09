pipeline {
  agent any
  stages {
    stage('CVS Checkout') {
      steps {
        echo 'Code Checkout'
        ws(dir: 'EMS') {
          echo 'CVS Checkout Completed'
        }

      }
    }
    stage('Initialize') {
      environment {
        AS5 = 'AS5_32'
        AS5_64 = 'AS5_64'
        AS6 = 'AS_32'
        AS6_64 = 'AS_64'
      }
      parallel {
        stage('Initialize') {
          steps {
            isUnix()
          }
        }
        stage('Docker Build Image') {
          steps {
            node(label: 'AS5') {
              echo 'AS5 Node Healthy'
            }

            node(label: 'AS5_64') {
              echo 'AS5_64'
            }

            node(label: 'AS6') {
              echo 'AS6 Node Ready'
            }

            node(label: 'AS6_64') {
              echo 'AS6_64 Build Node Ready'
            }

          }
        }
      }
    }
    stage('Build Job 12-2-0') {
      steps {
        build 'AS5'
        build 'AS5_64'
        build 'AS6'
        build 'AS6_64'
      }
    }
    stage('Status Reports') {
      parallel {
        stage('Status Reports') {
          steps {
            echo 'Build Success or Failure'
          }
        }
        stage('Success') {
          steps {
            echo 'Success '
          }
        }
        stage('Failed') {
          steps {
            waitForQualityGate true
          }
        }
      }
    }
    stage('Email Notification') {
      steps {
        echo 'Pass or Fail'
      }
    }
    stage('Packaging') {
      steps {
        echo 'Copy the Package as per Define Build'
      }
    }
    stage('Release Reports') {
      steps {
        archiveArtifacts(artifacts: 'Release 12-2-0', allowEmptyArchive: true, onlyIfSuccessful: true)
      }
    }
    stage('End') {
      steps {
        echo 'Task Completed'
      }
    }
  }
}