pipeline {
  agent any
  stages {
    stage('Config') {
      steps {
        sh 'echo nothing'
        sh 'echo $PERSON'
      }
    }
    stage('error') {
      environment {
        DEVICE = 'ABIGDEVICE'
      }
      steps {
        sh '''cd build

'''
        sh './build/prebuild.sh'
      }
    }
  }
  parameters {
    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
  }
}