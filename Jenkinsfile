pipeline {

    agent any

    environment {
        IMAGE_NAME = "your-dockerhub-user/jenkins-cicd-project"
        IMAGE_TAG  = "v1"
    }


    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/skumari323/jenkins-cicd-project.git'
            }
        }


        stage('Build Application') {
            steps {
                sh '''
                echo Building application
                '''
            }
        }


        stage('Docker Build') {
            steps {
                sh '''
                docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
                '''
            }
        }


        stage('Deploy DEV') {
            steps {
                sh '''
                echo Deploying to DEV environment

                kubectl apply -f dev.yaml
                '''
            }
        }


        stage('DEV Testing') {
            steps {
                sh '''
                echo Running DEV tests
                '''
            }
        }


        stage('Approval for PROD') {

            steps {

                input(
                    message: 'Deploy to Production?',
                    ok: 'Deploy'
                )

            }
        }


        stage('Deploy PROD') {

            steps {

                sh '''
                echo Deploying to PROD environment

                kubectl apply -f prod.yaml
                '''

            }
        }

    }


    post {

        success {
            echo "Pipeline completed successfully"
        }

        failure {
            echo "Pipeline failed"
        }

    }

}