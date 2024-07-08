pipeline {
    agent {
        label 'slave1'
    }

    environment {
        MVN_HOME = tool name: 'maven', type: 'maven'
        POM_FILE = 'pom.xml'
        NEXUS_TOKEN = 'nexus-token'
    }
    
    stages {
        stage('Code build using MAVEN') {
            steps {
                script {
                    sh "${env.MVN_HOME}/bin/mvn clean package"
                }
            }
        }

        stage('Extract POM Information') {
            steps {
                script {
                    def pom = readMavenPom file: "${POM_FILE}"
                    POM_GROUPID = pom.groupId
                    POM_VERSION = pom.version
                    POM_ARTIFACTID = pom.artifactId
                    POM_PACKAGING = pom.packaging
                }
            }
        }

        stage('Upload artifact to Nexus') {
            steps {
                script {
                    nexusArtifactUploader(
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        nexusUrl: '172.31.87.160',
                        credentialsId: "${env.NEXUS_TOKEN}",
                        groupId: "${POM_GROUPID}",
                        version: "${POM_VERSION}",
                        repository: 'pipelineapp1',
                        artifactId: "${POM_ARTIFACTID}",
                        type: "${POM_PACKAGING}",
                        file: "./target/${POM_ARTIFACTID}-${POM_VERSION}.${POM_PACKAGING}"
                    )
                }
            }
        }
    }
}
