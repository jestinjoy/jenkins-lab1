
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Build stage started'
                sh 'echo Preparing the project...'
                sh 'ls -la'
            }
        }

        stage('Test') {
            steps {
                echo 'Test stage started'

                sh '''
                    if [ -f README.md ]; then
                        echo "Test passed: README.md exists"
                    else
                        echo "Test failed: README.md is missing"
                        exit 1
                    fi
                '''
            }
        }

        stage('Finish') {
            steps {
                echo 'All stages completed successfully!'
            }
        }
    }
}
