pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'java:1.0'
    }

    stages {
        stage('Checkout') {
            steps {
                echo '🔄 Checking out source code...'
                git branch: 'main', url: 'https://github.com/Rohitkumarr29/simple-java-docker.git'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    echo '🐳 Starting Docker build...'
                    if (fileExists('Dockerfile')) {
                        sh '''
                            set -x
                            docker version
                            docker build -t ${DOCKER_IMAGE} .
                        '''
                    } else {
                        error "❌ Dockerfile not found in the workspace."
                    }
                }
            }
        }

        stage('Docker Run (Optional)') {
            steps {
                script {
                    echo '🚀 Running Docker container...'
                    sh '''
                        set -x
                        docker images
                        docker run --rm ${DOCKER_IMAGE}
                    '''
                }
            }
        }
    }

    post {
        success {
            echo '✅ Python application Docker image built and run successfully.'
        }
        failure {
            echo '❌ Docker build or run failed.'
        }
    }
}
