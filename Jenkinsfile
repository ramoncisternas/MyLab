pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    environment{
       ArtifactId = readMavenPom().getArtifactId()
       Version = readMavenPom().getVersion()
       Name = readMavenPom().getName()
       GroupId = readMavenPom().getGroupId()
    }
    stages {
        // Specify various stage with in stages
        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }
        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }
        // Stage3 : Publishing the artifacts to Nexus
        stage ('Publish to Nexus'){
            steps {
                script {
                def NexusRepo = Version.endsWith("SNAPSHOT") ? "VinaysDevOpsLab-SNAPSHOT" : "VinaysDevOpsLab-RELEASE"
                nexusArtifactUploader artifacts: 
                [[artifactId: 'VinayDevOpsLab', 
                classifier: '', 
                file: "target/${ArtifactId}-${Version}.war", 
                type: 'war']], 
                credentialsId: '8de8792b-b20f-4c0b-a726-db295f070340', 
                groupId: "${GroupId}", 
                nexusUrl: '172.20.10.134:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: "${NexusRepo}", 
                version: "${Version}"
            }
        }
        // Stage 4 : Print some information
        stage ('Print Environment variables'){
                    steps {
                        echo "Artifact ID is '${ArtifactId}'"
                        echo "Version is '${Version}'"
                        echo "GroupID is '${GroupId}'"
                        echo "Name is '${Name}'"
                    }
                }

//        // Stage3 : Publish the source code to Sonarqube
//        stage ('Sonarqube Analysis'){
//            steps {
//                echo ' Source code published to Sonarqube for SCA......'
//                withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
//                     sh 'mvn sonar:sonar'
//                }
//
//            }
//        }

        
        
    }

}
