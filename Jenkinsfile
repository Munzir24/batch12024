pipeline {
    agent {
  label 'slave1'
}
    environment {
        MVN_HOME = tool name: 'maven', type: 'maven'
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
                    sh "${env.MVN_HOME}/bin/mvn clean"
                }
            }
        }
    }
}
