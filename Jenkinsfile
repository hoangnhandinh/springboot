pipeline {

    agent any

    // environment {
    //     MYSQL_ROOT_LOGIN = credentials('mysql-root-login')
    // }
    // stages {

    //     stage('Packaging/Pushing imagae') {

    //         steps {
    //             withDockerRegistry(credentialsId: 'dockerhub', url: 'https://index.docker.io/v1/') {
    //                 sh 'docker build -t khaliddinh/springboot .'
    //                 sh 'docker push khaliddinh/springboot'
    //             }
    //         }
    //     }

        stage('Deploy HTTPD to DEV') {
            steps {
                echo 'Deploying and cleaning'
                sh 'docker image pull httpd:latest'
                sh 'docker container stop nhandinh-httpd || echo "this container does not exist" '
                sh 'echo y | docker container prune '
                sh "docker run --name nhandinh-httpd -p 8080:80 -d  httpd:latest"
            }
        }

    //     stage('Deploy Spring Boot to DEV') {
    //         steps {
    //             echo 'Deploying and cleaning'
    //             sh 'docker image pull khaliddinh/springboot'
    //             sh 'docker container stop khalid-springboot || echo "this container does not exist" '
    //             sh 'docker network create dev || echo "this network exists"'
    //             sh 'echo y | docker container prune '

    //             sh 'docker container run -d --rm --name khalid-springboot -p 8081:8080 --network dev khaliddinh/springboot'
    //         }
    //     }
 
    // }
    post {
        // Clean after build
        always {
            cleanWs()
        }
    }
}
