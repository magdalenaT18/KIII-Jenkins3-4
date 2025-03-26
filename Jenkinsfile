pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "magdalena18/kiii-jenkins"
        DOCKER_CREDENTIALS = "dockerhub"  // Ensure this exists in Jenkins credentials
        DOCKER_REGISTRY = "https://registry.hub.docker.com"
    }

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Build and Push Image') {
            when {
                branch 'dev'  // Runs only if the branch is 'dev'
            }
            steps {
                script {
                    echo "Building Docker image..."
                    app = docker.build("${DOCKER_IMAGE}")

                    echo "Pushing Docker image to Docker Hub..."
                    docker.withRegistry(DOCKER_REGISTRY, DOCKER_CREDENTIALS) {
                        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        app.push("${env.BRANCH_NAME}-latest")
                    }
                }
            }
        }
    }
}
