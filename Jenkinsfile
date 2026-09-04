pipeline {
    agent any

    environment {
        PATH = "/opt/homebrew/bin:/Applications/Docker.app/Contents/Resources/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                sh '''
                    docker --version
                '''
            }
        }

        stage('Terraform') {
            steps {
                echo 'Running Terraform...'
                dir('terraform') {
                    sh '''
                        terraform fmt -check
                        terraform init
                        terraform validate
                        terraform apply -auto-approve
                    '''
                }
            }
        }

        stage('Docker Compose') {
            steps {
                echo 'Running Docker Compose...'
                sh '''
                    docker compose version
                    docker compose up -d --build
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}