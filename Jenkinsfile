node {
    def app

    stage('Build image') {
        app = docker.build("mywebapp")
    }

    stage('Test image') {
        app.inside {
            sh 'echo "Test passed"'
        }
    }

    stage('Deploy image') {
        app.run("-p 8089:80 --env welcome_message='${welcome_message}'")
    }

    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}