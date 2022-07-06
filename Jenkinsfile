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

        // Stage3 : Publish the source code to Sonarqube
        stage ('Publish to nexus'){
            steps {
                    nexusArtifactUploader artifacts: [[artifactId: 'KshitijDevOpsLab', classifier: '', file: 'target/KshitijDevOpsLab-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: '60dd6ec6-ffe3-4779-bc02-4257ae230b1c', groupId: 'com.kshitijlab', nexusUrl: '172.20.10.72:8081', nexusVersion: 'nexus2', protocol: 'http', repository: 'KshitijDevOpsLab-SNAPSHOT', version: '0.0.4-SNAPSHOT'
                }
            }
        }

        //stage 4 : deploy
        stage ('Deploy'){
            steps{
                echo ' deploy......'
            }
        }
}