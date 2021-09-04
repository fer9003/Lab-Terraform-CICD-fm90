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
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/FernandoDevOpsLab-0.0.5-SNAPSHOT.war', type: 'war']], credentialsId: 'd3a7bf80-25b4-45f7-8c13-ed17743b4356', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.27:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'FernandoDevOps-SNAPSHOT', version: '0.0.5-SNAPSHOT'
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
