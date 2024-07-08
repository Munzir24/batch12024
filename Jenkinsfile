pipeline {
    agent {
        label 'slave1'
    }

    environment {
        MVN_HOME = tool name: 'maven', type: 'maven'
        POM_FILE = 'pom.xml'
        NEXUS_TOKEN = credentials('nexus-token')
    }
    stages {
        stage('Code build using MAVEN'){
            steps {
                script {
                    sh "${env.MVN_HOME}/bin/mvn clean package"
                }
            }
        }
    }
}
