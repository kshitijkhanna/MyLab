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

        // stage 1. Build -- maven plugin
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

        // Stage3 : Publish the source code to Sonarqube -- nexus plugin
        stage ('Publish to nexus'){
            steps {
                //script block required as we want to deal with repository where the code should be published.snapshot or release
                    script{
                            def NexusRepo = Version.endsWith("SNAPSHOT") ? "KshitijDevOpsLab-SNAPSHOT" : "KshitijDevOpsLab-RELEASE"
                            nexusArtifactUploader artifacts: 
                            [[artifactId: "${ArtifactId}", 
                            classifier: '', 
                            file: 'target/KshitijDevOpsLab-0.0.4-SNAPSHOT.war', 
                            type: 'war']], 
                            credentialsId: '60dd6ec6-ffe3-4779-bc02-4257ae230b1c', 
                            groupId: "${GroupId}", 
                            nexusUrl: '172.20.10.72:8081', 
                            nexusVersion: 'nexus3', 
                            protocol: 'http', 
                            repository: "${NexusRepo}", 
                            version: "${Version}"
                    }
                }
            }
        //stage 4 : print environment variables --pipeline utility plugin
        stage('print environment variables'){
            steps{
                echo "Artifact ID is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "Name is '${Name}'"
                echo "GroupID is '${GroupId}'"
            }
        }

        //stage 4 : deploy
        stage ('Deploy'){
            steps{
                echo ' deploy......'
            }
        }

        }

       
}