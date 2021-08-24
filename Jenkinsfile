pipeline {
    //Directivas
    agent any
    
    tools {
        maven 'maven'
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
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: 'ecda696c-7c23-4c69-a12c-1cf03c8cf7da', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.194:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'Fernando-DevOps-RELEASE', version: '0.0.4-SNAPSHOT'
            }
        }

        //Stage4: Deploying
        stage ('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}