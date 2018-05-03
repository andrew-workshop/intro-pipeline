pipeline {
  agent {
    label 'jdk8'
  }
  libraries {
    lib("SharedLibs")
  }
  stages {
    stage('Say Hello') {
      steps {
        echo "Hello ${params.Name}"
        echo "${TEST_USER_USR}"
        echo "${TEST_USER_PSW}"
        sh 'java -version'
      }
    }
    stage('Checkpoint') {
      agent none
        steps {
          checkpoint 'Checkpoint'
        }
    }
    stage('Shared Lib') {
         steps {
             helloWorld("Jenkins")
         }
    }
    stage('Testing') {
        parallel {
          stage('Java 9') {
            agent { label 'jdk9' }
            steps {
              container('maven9') {
                sh 'mvn -v'
              }
            }
          }
          stage('Java 8') {
            agent { label 'jdk8' }
            steps {
              container('maven8') {
                sh 'mvn -v'
              }
            }
          }
        }
      }
  }
  environment {
    MY_NAME = 'Andrew'
    TEST_USER = credentials('test-user')
  }
  parameters {
    string(name: 'Name', defaultValue: 'whoever', description: 'Who should I say hi to?')
  }
  post {
    aborted {
      echo 'Why didn\'t you push my button?'
    }
  }
}
