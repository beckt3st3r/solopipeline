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
        stage('error') {
          steps {
            script {
              env.b = build(job: 'item2', propagate: false,
               parameters: [string(name: 'passed_build_number_param', value: String.valueOf(PERSON))]).result
            }
            echo "$env.b"
            if(env.b == 'FAILURE'){
              echo "First job failed"
              currentBuild.result = 'UNSTABLE' // of FAILURE
            }
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
