pipeline {
    agent any
    
    stages {

        stage('Deploy HTTPD to DEV') {
            steps {
                echo 'Deploying and cleaning'
                sh 'docker image pull httpd:latest'
                sh 'docker container stop nhandinh-httpd || echo "this container does not exist" '
                sh 'echo y | docker container prune '
                sh "docker run --name nhandinh-httpd -p 8080:80 -d  httpd:latest"
            }
        }

    }
    post {
        // Clean after build
        always {
            cleanWs()
        }
    }
}
