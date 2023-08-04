pipeline {
    agent any
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerHub')
  }
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/Akash1582/node-todo-cicd.git", branch: "master"
            }
        }
        stage("Build and Test"){
            steps{
                sh "docker build . -t node-app-test-new"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                sh "docker tag node-app-test-new akash1582/node-app-test-new:latest"
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh "docker push akash1582/node-app-test-new:latest"
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
    post {
    always {
      sh 'docker logout'
    }
  }
}
