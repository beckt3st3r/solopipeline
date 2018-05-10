pipeline {
  agent any
  stages {
    stage('Config') {
      steps {
        sh 'echo nothing'
        sh 'echo $PERSON'
      }
    }
    stage('PreBuild') {
      parallel {
        stage('PreBuild') {
          environment {
            DEVICE = 'ABIGDEVICE'
          }
          steps {
            sh './build/prebuild.sh'
          }
        }
        stage('PreBuildDev2') {
          environment {
            DEVICE = 'device2'
          }
          steps {
            sh './build/prebuild.sh'
          }
        }
        stage('PreBuildDev3') {
          environment {
            DEVICE = 'Device3'
          }
          steps {
            sh './build/prebuild.sh'
          }
        }
      }
    }
    stage('Build') {
      steps {
        sh './build/build.sh'
      }
    }
  }
  parameters {
    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
  }
}