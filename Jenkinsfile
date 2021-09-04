pipeline {
    //Directivas
    agent any
    
    tools {
        maven 'maven'
    }
    
    
    environment {
        ArtifactId = readMavenPom().getArtifactId()
        Version = readMavenPom().getVersion()
        Name = readMavenPom().getName()
        GroupId = readMavenPom().getGroupId()
    }

    stages {
        //stage 1: Build
        stage ('Build') {
            steps {
                sh 'mvn clean install package'
            }
        }

        //Stage 2: Testing
        stage ('Test') {
            steps {
                echo 'Testing'
            }
        }

        //Stage 3: Public de artifacts to Nexus
        stage ('Publish to Nexus') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.5-SNAPSHOT.war', type: 'war']], credentialsId: 'd3a7bf80-25b4-45f7-8c13-ed17743b4356', groupId: 'com.vinaysdevops.lab', nexusUrl: '172.20.10.27:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'FernandoDevOps-SNAPSHOT', version: '0.0.5-SNAPSHOT'
            }
        }
        
        //Stage 4:
        
        stage ('Print Environment Variables') {
            steps {
                echo "Artifact ID is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "GroupID is '${GroupId}'"
                echo "Name is '${Name}'"
            }
        }
        
        
        
        //Stage5: Deploying
        stage ('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
