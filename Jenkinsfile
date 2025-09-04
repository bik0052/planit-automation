pipeline {
  agent any
  environment {
    HEADLESS = 'true'
  }
  stages {
    stage('Checkout') {
      steps { checkout scm }
    }
    stage('Build & Test (Headless Chrome)') {
      steps {
        sh 'mvn -version'
        sh 'mvn -B clean test -Dheadless=true'
      }
    }
  }
  post {
    always {
      archiveArtifacts artifacts: 'target/surefire-reports/**', fingerprint: true
      junit 'target/surefire-reports/*.xml'
    }
  }
}
