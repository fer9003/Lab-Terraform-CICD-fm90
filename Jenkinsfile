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

        //Stage3: Deploying
        stage ('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}