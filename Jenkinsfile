pipeline{
    agent any 
    stages(){
        stage("Code Cloning From Github"){
            steps{
                git url:"https://github.com/krishvaghela1212/django-notes-app.git" ,branch: "main"
                
            }
        }
        stage("Build"){
            steps{
                echo "Building the image"
                sh "docker build -t my-note-app ."
                
                
            }
        }
     stage("Push to Docker Hub"){
            steps{
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest "
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/my-note-app:latest "
                }
                
            }
        }
        stage("Deploying code "){
            steps{
                echo "Deployment of Code "
                sh "docker run -d  --name my-note-app -p 8000:8000 krish32/my-note-app:latest"
            }
        }
    }
}
