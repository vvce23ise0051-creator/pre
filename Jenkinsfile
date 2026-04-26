pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'nettarshama05/myapp:v1'
    }

    stages {

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-cred',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    bat '''
                    echo %PASS%> pass.txt
                    type pass.txt | docker login -u %USER% --password-stdin
                    del pass.txt
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE% .'
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push %DOCKER_IMAGE%'
            }
        }
    }
}
