```groovy
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ad4r5h/flask-app:latest ./app'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push ad4r5h/flask-app:latest'
            }
        }
    }

    post {
        success {
            echo 'Jenkins Pipeline completed successfully!'
        }

        failure {
            echo 'Jenkins Pipeline failed!'
        }
    }
}
```
