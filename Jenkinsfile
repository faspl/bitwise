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

          }
        }
      }
    }
  }
}