pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                dir('app') {
                    script {
                        def dockerComposeTest = sh(script: 'docker-compose -f docker-compose.yml up --abort-on-container-exit', returnStatus: true)

                        if (dockerComposeTest != 0) {
                            error('Docker Compose test failed')
                        }
                    }
                }
            }
        }

        stage('Build') {
            steps {
                dir('app') {
                    script {
                        def dockerComposeBuild = sh(script: 'docker-compose -f docker-compose.yml build', returnStatus: true)

                        if (dockerComposeBuild != 0) {
                            error('Docker Compose build failed')
                        }
                    }
                }
            }
        }
    }
}

