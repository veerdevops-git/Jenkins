pipeline{
    agent { label 'node-agent' }
    
    stages{
        stage("code"){
            steps{
                echo "Cloning gitHub repo"
                git url: "https://github.com/sayalishewale/jenkins-CICD.git",branch:'main'
            } 
        }
        stage("build"){
            steps{
                echo "building code"
                sh "docker build -t sayalishewale/node-app ."
                
                
            }
            
        }
        
        stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPass' , usernameVariable: 'dockerHubUser')]) {
                 sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                 sh "docker push sayalishewale/node-app:latest"
                }
            }   
                
        }
        stage("test"){
            steps{
                echo "testing code"
                
            }
            
        }
        stage("deploy"){
            steps{
                echo "deploying code"
                sh "docker-compose down && docker-compose up --no-deps --build -d"
                
            }
            
        }
    }
    
}
