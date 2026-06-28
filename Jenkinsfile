@Library("shared") _
pipeline{
    agent any
    environment{
        SONAR_HOME= tool "sonar"
       }
    stages{
        stage("Cloning The Project"){
            steps{
              script{
                clone("https://github.com/shashankcodes-10/two-tier-flask-app.git" , "master")
              }
            }
        }
        stage("Sonarqube Quality Analysis"){
            steps{
                  script{
                      sonarqube_analysis("sonar","two-tier","two-tier")
                  }
                }
            }
        stage("Sonar Quality Gates Scan"){
            steps{
                script{
                    sonar_quality_gate()
                }
                }
            }
        stage("OWASP Dependency Check"){
            steps{
                script{
                    owasp_check("owasp")
                }
            }
        }
        stage("Trivy FileSystem Scan"){
            steps{
               script{
                   trivy_fs_scan()
               }
            }
        }
        stage("Building The Image"){
            steps{
                script{
               docker_build("two-app")
                }
            }
        }
        stage("Trivy Image Scan"){
              steps{
                     script{
                         trivy_image_scan("two-app")
                     }
                }
           }
        stage("Pushing To dockerHub"){
            steps{
                script{
                docker_hub_push("dockerhubCreds","two-app")
                }
            }
        }
        stage("Running The image"){
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
