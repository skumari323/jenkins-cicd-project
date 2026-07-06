pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/skumari323/jenkins-cicd-project.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Building project..."'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t jenkins-cicd-project:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run jenkins-cicd-project:latest'
            }
        }
    }
}
