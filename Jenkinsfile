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
            sh 'echo $DEVICE > device.txt'
          }
        }
        stage('PreBuildDev2') {
          environment {
            DEVICE = 'device2'
          }
          steps {
            sh './build/prebuild.sh'
            sh 'return 0'
          }
        }
        stage('PreBuildDev3') {
          environment {
            DEVICE = 'Device3'
          }
          steps {
            sh './build/prebuild.sh'
            sh 'echo $DEVICE > device3.txt'
          }
        }
        stage('') {
          steps {
            build 'item2'
          }
        }
      }
    }
    stage('Build') {
      environment {
        TYPE = 'normal'
      }
      steps {
        sh './build/build.sh'
        sh 'DEVICE=$(cat device.txt) && echo $DEVICE'
      }
    }
  }
  parameters {
    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
  }
}