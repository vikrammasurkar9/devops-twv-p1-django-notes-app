pipeline{
    agent any
    
    stages{
        stage("clone code "){
            steps{
               echo "cloning code" 
              git url:"https://github.com/vikrammasurkar9/devops-twv-p1-django-notes-app.git",branch:"main"
            }
              }
         stage("Build"){
             steps{
                echo"building code"
                sh "docker build -t my-dotes-app ."
            }
              }
        stage("Push to Docker Hub"){
             steps{
                echo "pushing image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh"docker tag my-dotes-app ${env.dockerHubUser}/my-dotes-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-dotes-app:latest"
                }
            }
              }
         stage("Deploy"){
             steps{
                echo"deploying the container"
                sh "docker-compose down && docker-compose up -d"
            }
              }
      }
        
}
