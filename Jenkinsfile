pipeline{
    agent any
    stages{
        stage("code"){
            steps{
                echo "Pull Code Successfully"
                git url:"https://github.com/vikrammasurkar9/devops-twv-p1-django-notes-app.git",branch:"main"
                
            }
        }
        stage("Builds"){
            steps{
               echo "Building Code" 
               sh "docker build -t my-notes-app ."
            }
        }
        
        stage("Push to Docker Hub"){
            steps{
               echo "Pushing Code To Docker Hub" 
               
               withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")])
               {
                   sh"docker tag my-notes-app ${env.dockerHubUser}/my-notes-app:v2"
                   sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                   sh "docker push ${env.dockerHubUser}/my-notes-app:v2"
               }
                echo "Connected To  To Docker Hub" 
            }
        }
        stage("Deploy"){
            steps{
                echo "Deploying container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
        
    }
}
