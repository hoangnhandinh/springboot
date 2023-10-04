pipeline {

    agent any

    environment {
        MYSQL_ROOT_LOGIN = credentials('mysql-root-login')
    }
    stages {

        stage('Packaging/Pushing imagae') {

            steps {
                withDockerRegistry(credentialsId: 'dockerhub', url: 'https://index.docker.io/v1/') {
                    sh 'docker build -t nhandinh4747/springboot .'
                    sh 'docker push nhandinh4747/springboot'
                }
            }
        }

        stage('Deploy MySQL to DEV') {
            steps {
                echo 'Deploying and cleaning'
                sh 'docker image pull mysql:8.0'
                sh 'docker network create dev || echo "this network exists"'
                sh 'docker container stop nhandinh4747-mysql || echo "this container does not exist" '
                sh 'echo y | docker container prune '
                sh 'docker volume rm nhandinh4747-mysql-data || echo "no volume"'

                sh "docker run --name nhandinh4747-mysql --rm --network dev -v nhandinh4747-mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=${MYSQL_ROOT_LOGIN_PSW} -e MYSQL_DATABASE=db_example  -d mysql:8.0 "
                sh 'sleep 20'
                sh "docker exec -i nhandinh4747-mysql mysql --user=root --password=${MYSQL_ROOT_LOGIN_PSW} < script"
            }
        }

        stage('Deploy Spring Boot to DEV') {
            steps {
                echo 'Deploying and cleaning'
                sh 'docker image pull nhandinh4747/springboot'
                sh 'docker container stop nhandinh4747-springboot || echo "this container does not exist" '
                sh 'docker network create dev || echo "this network exists"'
                sh 'echo y | docker container prune '

                sh 'docker container run -d --rm --name nhandinh4747-springboot -p 8081:8080 --network dev nhandinh4747/springboot'
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
