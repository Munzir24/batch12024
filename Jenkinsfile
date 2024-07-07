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
                    sh "${env.MVN_HOME}/bin/mvn clean install"
                }
            }
        }
        stage('Sonar Analysis'){
            steps {
                script {
                    sh """
                    #!/bin/bash
                    echo "Executing sonar cli"
                    sonar-scanner \
                    -Dsonar.projectKey="munzirbatch1aws2024org_javaapp1"  \
                    -Dsonar.sources="./target"   \
                    -Dsonar.host.url="https://sonarcloud.io" \
                    -Dsonar.branch.target="master" \
                    -Dsonar.branch.name="release" \
                    -Dsonar.login=${env.SONAR_TOKEN} \
                    -Dsonar.organization="munzirbatch1aws2024org"
                    """
                }
            }
        }
    }
}
