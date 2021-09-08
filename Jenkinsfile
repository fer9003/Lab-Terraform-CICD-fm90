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
                script {
                    def NexusRepo = Version.endsWith("SNAPSHOT") ? "FernandoDevOps-SNAPSHOT" : "Fernando-DevOps-RELEASE"
                    nexusArtifactUploader artifacts:
                    [[artifactId: "${ArtifactId}", 
                    classifier: '', 
                    file: "target/${ArtifactId}-${Version}.war", 
                    type: 'war']], credentialsId: 'd3a7bf80-25b4-45f7-8c13-ed17743b4356', 
                    groupId: "${GroupId}", 
                    nexusUrl: '172.20.10.124:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: "${NexusRepo}", 
                    version: "${Version}"
                }
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
                sshPublisher(publishers: 
                [sshPublisherDesc(
                    configName: 'AnsibleController',
                    transfers: [
                        sshTransfer(
                            cleanRemote: false,
                            execCommand: 'ansible-playbook /opt/playbooks/downloadanddeploy.yaml -i /opt/playbooks/hosts',
                            execTimeout: 120000
                        )
                    ],
                    usePromotionTimestamp: false,
                    useWorkspaceInPromotion: false,
                    verbose: false)
                    ])
            }
        }
    }
}
