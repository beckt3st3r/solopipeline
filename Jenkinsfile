pipeline {
  agent any
  stages {
    stage('Config') {
      steps {
        sh 'echo nothing'
      }
    }
  }
  parameters {
    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
  }
}