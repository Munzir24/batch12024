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
                    def pom = readMavenPom file: "${env.POM_FILE}"
                    env.POM_GROUPID = pom.groupId
                    env.POM_VERSION = pom.version
                    env.POM_ARTIFACTID = pom.artifactId
                    env.POM_PACKAGING = pom.packaging
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
                        groupId: "${env.POM_GROUPID}",
                        version: "${env.POM_VERSION}",
                        repository: 'pipelineapp1',
                        artifactId: "${env.POM_ARTIFACTID}",
                        type: "${env.POM_PACKAGING}",
                        file: "./target/${env.POM_ARTIFACTID}-${env.POM_VERSION}.${env.POM_PACKAGING}"
                    )
                }
            }
        }
    }
}
