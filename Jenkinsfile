pipeline {
    agent {
        label 'slave1'
    }

    environment {
        MVN_HOME = tool name: 'maven', type: 'maven'
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
        stage('Upload artificat to Nexus'){
            steps {
                script {
                    nexusArtifactUploader(
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        nexusURL: '172.31.87.160',
                        credentials: "${env.NEXUS_TOKEN}",
                        Group_ID: "${POM_GROUPID}",
                        Version: "${POM_VERSION}",
                        Repository: 'pipelineapp1',
                        ArtifactId: ${POM_ARTIFACTID},
                        Type: ${POM_PACKAGING},
                        File:  ./target/${POM_ARTIFACTID}-${POM_VERSION}.${POM_PACKAGING}
                        )
                }
            }
        }
    }
}
