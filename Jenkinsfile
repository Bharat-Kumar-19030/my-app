pipeline{
    agent any
    stages{
        stage('checkout'){
            steps{
                git branch: 'main',
                 url: 'https://github.com/Bharat-Kumar-19030/my-app.git'
            }
        }
        stage('build'){
            steps{
                bat 'npm install'
            }
        }
        stage('DockerLogin'){
            withCredentials([
                    usernamePassword(
                        credentialsId:'docker-creds',
                        usernameVariable:'USER',
                        passwordVariable:'PASS'
                    )
                ]){
                bat ''' 
                    echo %PASS% | docker login -u %USER% --password-stdin
                '''
            }
        }
        stage('BuildDockerImageAndPush'){
            steps{
                bat 'docker build -t %USER%/my-app:latest .'
                bat 'docker push %USER%/my-app:latest'
            }
        }
        stage('Deploy'){
            steps{
                sh 'docker service create -d -p 5000:5000 my-app:latest'
            }
        }
    }
}