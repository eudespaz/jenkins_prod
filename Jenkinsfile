pipeline {
    agent any

    stages {

        stage('Get Source') {
            steps {
                git url: 'https://github.com/eudespaz/jenkins_prod.git', branch: 'master'
            }
        }
    
        stage('Docker Build') {
            steps {
                script {
                    dockerapp = docker.build("eudespaz/jenkins-prod:${env.BUILD_ID}",
                    '-f ./C:/Users/eudes.paz/jenkins_prod/Dockerfile/Dockerfile .')
                }
            }
        }
        
        stage('Docker Push Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'DockerHub') {
                    dockerapp.push('latest')
                    dockerapp.push("${env.BUILD_ID}")

                    }
                }
            }       
        }
    }
}

