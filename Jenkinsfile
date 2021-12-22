pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
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
        stage ('Deploy'){
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: '8de8792b-b20f-4c0b-a726-db295f070340', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.134:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'DevOpsLab-SNAPSHOT', version: '0.0.4-SNAPSHOT'
            }
        }

//        // Stage4 : Deploying
//        stage ('Deploy'){
//            steps {
//                echo ' deploying......'
//
//            }
//        }
//
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
