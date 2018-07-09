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
  }
}