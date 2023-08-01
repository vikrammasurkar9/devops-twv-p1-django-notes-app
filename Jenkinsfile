pipeline{
 agent any
    stages{
        stage("code"){
            steps{
                echo "cloning code"
               git url:"https://github.com/vikrammasurkar9/devops-twv-p1-django-notes-app.git",branch:"main"
            }
        }
        stage("Build"){
             steps{
            echo "Building Code"
            sh "docker build -t my-notes-app ."
             }
        }
        stage("Push to Docker Hub"){
             steps{
            echo "Pushing imege to docker hub"
            withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
               sh "docker tag my-notes-app ${env.dockerHubUser}/my-notes-app:v1"
               sh "docker login -u ${env.dockerHubUser} -p ${dockerHubPass}"
               sh "docker push ${env.dockerHubUser}/my-notes-app:v1"
                
            }
             }
        }
        stage("Deploy"){
             steps{
            echo "Deolpying the container"
           
            sh "docker-compose down && docker-compose up -d"
             }
        }
    }


}
