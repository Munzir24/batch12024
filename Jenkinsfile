pipeline {
    agent {
  label 'slave'
}
    environment {
        MVN_HOME = tool name: 'maven', type: 'maven'
        SONAR_TOKEN = credentials('sonar-token')
    }

    stages {
        stage('Code Checkout to release branch'){
            steps {
                script {
                    // Checkout code from the repository
                    git url: 'https://github.com/Munzir24/myweb.git'
                }
            }
        }
        stage('Code build'){
            steps {
                script {
                    // Executing Code build
                    sh "${env.MVN_HOME}/bin/mvn clean package"
                }
            }
        }
    }
}
