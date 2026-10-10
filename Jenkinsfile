
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code is checked out by Jenkins.'
                sh 'ls -la'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-docker-lab:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                    docker rm -f jenkins-docker-lab || true

                    docker run -d \
                        --name jenkins-docker-lab \
                        --restart unless-stopped \
                        -p 8082:80 \
                        jenkins-docker-lab:latest
                '''
            }
        }

        stage('Test Application') {
            steps {
                sh '''
                    sleep 2
                    curl --fail http://localhost:8082/
                '''
            }
        }
    }

    post {
        success {
            echo 'Application deployed successfully!'
            echo 'Open http://localhost:8082 in your browser.'
        }

        failure {
            echo 'Pipeline failed. Check the Console Output.'
        }
    }
}
