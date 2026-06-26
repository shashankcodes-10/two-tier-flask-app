pipeline{
    agent any
    stages{
        stage("cloneing the project"){
            steps{
                git url :"https://github.com/shashankcodes-10/two-tier-flask-app.git" , branch : "master"
            }
        }
        stage("building the image"){
            steps{
               sh "docker build -t two-app:latest ."
            }
        }
        stage("pushing to docker hub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"dockerhubCreds",
                    usernameVariable:"dockerHubuser",
                    passwordVariable:"dockerHubpass"
                    )]){
                          sh '''
                           echo "$dockerHubpass" | docker login -u "$dockerHubuser" --password-stdin
                           '''

                        sh "docker image tag two-app:latest ${env.dockerHubuser}/two-app"
                        sh "docker push ${env.dockerHubuser}/two-app:latest"
                }
            }
        }
        stage("running the image"){
            steps{
                sh "docker compose up -d --build "
            }
        }
    }
    
}
