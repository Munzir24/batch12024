pipeline {
    agent any
    parameters {
  choice choices: ['dev', 'prod', 'sit'], name: 'ENV'
}
    stages {
        stage('Welcome') {
            steps {
                script {
                    println "Hi how are you?"
                    println "Your chosen environment is ${params.ENV}"
                }
            }
        }
    }
}
