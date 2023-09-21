pipeline{
    agent {
        label 'agent-dev'
    }
    
    stages{
        stage ('Code'){
            steps {
                git url:'https://github.com/paragpallavsingh/node-todo-cicd.git', branch: 'master'
            }
        }
        stage ('Build and Test'){
            steps {
                sh 'docker build . -t paragpallavsingh/node-todo:latest'
            }
        }
        stage ('Login and push'){
            steps {echo 'Login into Dockerhub'
            withCredentials([usernamePassword (credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                sh "docker push paragpallavsingh/node-todo:latest"
            }
            }
        }
        stage ('Deploy'){
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
