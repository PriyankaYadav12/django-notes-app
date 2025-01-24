@Library('Shared') _
pipeline {
    agent {label "linux"}

    stages {
        stage("hello") {
            steps{
                script{
                    hello()
                }
            }
        }
        stage('Source Code - GitHub') {
            steps {
                script { 
                 
                   clone('https://github.com/PriyankaYadav12/django-notes-app.git', 'main')
                }
            }
        }
       stage('Build') {
            steps {
                script {
                   docker_build("notes-app", "latest",  "priyankayadav08")
                }
              
            }
        }
        stage('Push Image - DockerHub ') {
            steps {
                script {
                    docker_push('notes-app', 'latest', 'priyankayadav08')
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'DeployApplication'
                //sh 'docker run -d -p 8000:8000 notes-app:latest'
                sh 'docker-compose down'
                sh 'docker-compose up -d'
            }
        }
    }
}
