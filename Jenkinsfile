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
      }
    }
  }
}