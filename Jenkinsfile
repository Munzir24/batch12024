pipeline {
    agent {
        label "slave1"
    }
    environment {
        MVN_HOME = tool name: 'maven', type: 'maven'
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "172.31.87.160"
        NEXUS_REPOSITORY = "pipelineapp1"
        NEXUS_CREDENTIAL_ID = "nexus-token"
        JAVA_HOME = "/usr/lib/jvm/java-11-openjdk-11.0.23.0.9-2.amzn2.0.1.x86_64/"
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }
    stages {
        stage("Clone code from VCS") {
            steps {
                script {
                    git url: 'https://github.com/Munzir24/myweb.git'
                }
            }
        }
        stage("Maven Build") {
            steps {
                script {
                    sh "${env.MVN_HOME}/bin/mvn clean package"
                }
            }
        }
        stage("Publish to Nexus Repository Manager") {
            steps {
                script {
                    pom = readMavenPom file: "pom.xml";
                    filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    artifactPath = filesByGlob[0].path;
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                        nexusArtifactUploader(
                            nexusVersion: "${env.NEXUS_VERSION}",
                            protocol: "${env.NEXUS_PROTOCOL}",
                            nexusUrl: "${env.NEXUS_URL}",
                            groupId: pom.groupId,
                            version: pom.version,
                            repository: "${env.NEXUS_REPOSITORY}",
                            credentialsId: "${env.NEXUS_CREDENTIAL_ID}",
                            artifacts: [
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: artifactPath,
                                type: pom.packaging],
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: "pom.xml",
                                type: "pom"]
                            ]
                        );
                    } else {
                        error "*** File: ${artifactPath}, could not be found";
                    }
                }
            }
        }
    }
}
