pipeline {
    agent any

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
                    export PATH="/Applications/Docker.app/Contents/Resources/bin:$PATH"
                    docker --version
                '''
            }
        }

        stage('Terraform') {
            steps {
                echo 'Running Terraform...'
                dir('terraform') {
                    sh '''
                        export PATH="/Applications/Docker.app/Contents/Resources/bin:$PATH"
                        terraform fmt -check
                        terraform init
                        terraform validate
                    '''
                }
            }
        }

        stage('Docker Compose') {
            steps {
                echo 'Checking Docker Compose...'
                sh '''
                    export PATH="/Applications/Docker.app/Contents/Resources/bin:$PATH"
                    docker compose version
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