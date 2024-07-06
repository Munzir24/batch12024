pipeline {
    agent any
    environment {
        JAVA_HOME = "/usr/bin/java"
    }
    
    parameters {
  choice choices: ['dev', 'prod', 'sit'], name: 'ENV'
}
    stages {
        stage('Welcome') {
            steps {
                script {
                    println "Hi how are you?"
                    println "Your chosen environment is ${params.ENV}"
                    println "Your Java Home Path is ${env.JAVA_HOME}"
                }
            }
        }
    }
}
