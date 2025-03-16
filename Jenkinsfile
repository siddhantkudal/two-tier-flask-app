pipeline{
    agent { label "dev"};
    stages{
        stage("clone"){
            steps{
                
                  echo "Clone the build"
                  git url: "https://github.com/siddhantkudal/two-tier-flask-app.git", branch: "master"
            }
            
          
            
        }
        stage("Build"){
            steps{
                echo "Build is started"
                sh "docker build -t python-two-tier:latest ."
            }
            
            
        }
        stage("Push"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"dockerhubCreds",
                    passwordVariable: "dockerpassword",
                    usernameVariable: "dockerusername"
                )]){
                    
                    echo "Docker images to dockerhub"
                    sh "docker login -u ${env.dockerusername} -p ${env.dockerpassword}"
                    sh "docker image tag python-two-tier ${env.dockerusername}/python-two-tier"
                    sh "docker push ${env.dockerusername}/python-two-tier:latest"
                }
               
            }
            
        }
        stage("stage 4"){
            steps{
                echo "pull and start docker container"
                sh "docker compose up -d"
            }
            
        }
        
    }
}
