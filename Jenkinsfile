pipeline {
  agent {
    label 'jdk9'
  }
  stages {
    stage('Say Hello') {
      steps {
        echo 'Hello there'
        sh 'java -version'
      }
    }
  }
}