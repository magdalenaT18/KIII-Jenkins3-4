pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "magdalena18/kiii-jenkins"
        DOCKER_CREDENTIALS = "dockerhub"  // Make sure this credential exists in Jenkins
        DOCKER_REGISTRY = "https://registry.hub.docker.com"
    }

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Build image') {
            steps {
                script {
                    app = docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Push image') {
            steps {
                script {
                    docker.withRegistry(DOCKER_REGISTRY, DOCKER_CREDENTIALS) {
                        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        app.push("${env.BRANCH_NAME}-latest")
                    }
                }
            }
        }
    }
}
