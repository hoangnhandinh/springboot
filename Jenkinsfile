pipeline {
    agent any
    
    stages {

        // stage('Packaging/Pushing imagae') {

        //     steps {
        //         withDockerRegistry(credentialsId: 'dockerhub', url: 'https://index.docker.io/v1/') {
        //             sh 'docker build -t nhandinh4747/springboot .'
        //             sh 'docker push nhandinh4747/springboot'
        //         }
        //     }
        // }

        // stage('Deploy MySQL to DEV') {
        //     steps {
        //         echo 'Deploying and cleaning'
        //         sh 'docker image pull mysql:8.1'
        //         sh 'docker network create dev || echo "this network exists"'
        //         sh 'docker container stop nhandinh-mysql || echo "this container does not exist" '
        //         sh 'echo y | docker container prune '
        //         sh 'docker volume rm nhandinh-mysql-data || echo "no volume"'

        //         sh "docker run --name nhandinh-mysql --rm --network dev -v nhandinh-mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=Elcom@123 -e MYSQL_DATABASE=db_example  -d mysql:8.1 "
        //         sh 'sleep 20'
        //         sh "docker exec -i nhandinh-mysql mysql --user=root --password=Elcom@123 < script"
        //     }
        // }

        stage('Deploy Spring Boot to DEV') {
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
