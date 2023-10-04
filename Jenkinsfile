pipeline{
    agent any
    stages{
        stage('Code-Clone'){
            steps{
                echo 'Cloning the code'
                git url: 'https://github.com/harsh-learner/node-todo-cicd.git', branch: 'master'
                
            }
            
        }
        stage('Building the image'){
           steps{
               echo 'Building the image'
               sh 'docker build -t node-todo-app .'
                
            } 
            
        }
        stage('Pushing image to Dockerhub'){
            steps{
                echo 'Pushing image to Dockerhub'
                withCredentials([usernamePassword(credentialsId: "dockerHub", passwordVariable:"dockerHubPass", usernameVariable:"dockerHubUser")]){
                    sh "docker tag node-todo-app ${env.dockerHubUser}/node-todo-app:latest"
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/node-todo-app:latest"
                }
                
            }
            
        }
        stage('Deploying Container'){
            
            steps{
                echo 'Deploying the container'
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
    }
}
