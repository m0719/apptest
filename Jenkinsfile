pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/m0719/apptest.git'
            }
        }
        
        stage('Check Docker and Docker Compose') {
            steps {
                script {
                    def dockerInstalled = sh(script: "docker --version", returnStatus: true) == 0
                    def dockerComposeInstalled = sh(script: "docker-compose --version", returnStatus: true) == 0

                    if (!dockerInstalled) {
                        error('Docker is not installed')
                    }
                    if (!dockerComposeInstalled) {
                        error('Docker Compose is not installed')
                    }
                }
            }
        }
        
        stage('Check Python') {
            steps {
                script {
                    def pythonInstalled = sh(script: "python --version", returnStatus: true) == 0

                    if (!pythonInstalled) {
                        error('Python is not installed')
                    }
                }
            }
        }

        stage('Build and Test') {
            steps {
                script {
                    dockerComposeBuild = sh(script: 'docker-compose build', returnStatus: true)
                    dockerComposeTest = sh(script: 'docker-compose up --abort-on-container-exit', returnStatus: true)

                    if (dockerComposeBuild != 0) {
                        error('Docker Compose build failed')
                    }
                    if (dockerComposeTest != 0) {
                        error('Docker Compose test failed')
                    }
                }
            }
        }
    }
}

