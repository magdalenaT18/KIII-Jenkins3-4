node {
    def branchName = env.BRANCH_NAME ?: 'unknown'  // Default to 'unknown' if null
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("magdalena18/kiii-jenkins")
    }

    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${branchName}-${env.BUILD_NUMBER}")
            app.push("${branchName}-latest")
        }
    }
}
