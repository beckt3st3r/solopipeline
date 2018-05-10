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
            sh 'echo $DEVICE > device2.txt'
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
      }
    }
    stage('Build') {
      environment {
        TYPE = 'normal'
      }
      steps {
        sh './build/build.sh'
        sh 'device=\'cat device.txt\' && echo device'
      }
    }
  }
  parameters {
    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
  }
}