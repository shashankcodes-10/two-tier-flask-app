@Library("shared") _
pipeline{
    agent any
    stages{
        stage("cloning the project"){
            steps{
              script{
                clone("https://github.com/shashankcodes-10/two-tier-flask-app.git" , "master")
              }
            }
        }
        stage("building the image"){
            steps{
                script{
               docker_build("two-app")
                }
            }
        }
        stage("pushing to docker hub"){
            steps{
                script{
                docker_hub_push("dockerhubCreds","two-app")
                }
            }
        }
        stage("running the image"){
            steps{
                script{
                docker_run()
                }
            }
        }
        }
   post{
      success{
                script{
                   post_success()
                }
            }
      failure{
                script{
                   post_failure()
                }
            }        
        }
}
