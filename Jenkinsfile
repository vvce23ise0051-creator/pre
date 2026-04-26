pipeline{
    agent any
    environment{
        DOCKER_IMAGE='nettarshama05/myapp:v1'
    }
    stages{
        stage('Login to DockerHub'){
            steps{
                withcredentialsId([usernamePassword(
                    credentialsId :'docker_cred',
                    usernameVariable :'USER',
                    passwordVariable :'PASS'
                )])
                {
                    bat ' ' '
                    echo %PASS%> pass.txt
                    type pass.txt |docker login -u %USER% --password-stdin
                    del pass.txt
                    ' ' '
                    
                }
            }
        }
        stage('Build docker image'){
            steps{
                bat 'docker build image -t %DOCKER_IMAGE% .'
            }
        }
        stage('Push docker image'){
            steps{
                bat 'docker push %DOCKER_IMAGE'
            }
        }
    }
}