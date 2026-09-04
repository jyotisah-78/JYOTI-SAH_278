pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                sh 'docker --version'
            }
        }

        stage('Terraform') {
            steps {
                echo 'Running Terraform...'
                dir('terraform') {
                    sh 'terraform fmt -check'
                    sh 'terraform init'
                    sh 'terraform validate'
                }
            }
        }

        stage('Docker Compose') {
            steps {
                echo 'Checking Docker Compose...'
                sh 'docker compose version'
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