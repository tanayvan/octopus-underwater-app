pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
         stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }

        stage('Build') { 
            steps { 
                script{
                 app = docker.build("underwater")
                 docker.withRegistry('public.ecr.aws/d0u4c9c7/node-app', 'ecr:us-east-2:aws-credentials') {
                 app.push("${env.BUILD_NUMBER}")
                 app.push("latest")
                 }
                }
            }
        }
        stage('Deploy') {
            steps {
                script{
                    docker.withRegistry('public.ecr.aws/d0u4c9c7/node-app', 'ecr:us-east-2:aws-credentials') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                    }
                }
            }
        }
    }
}
