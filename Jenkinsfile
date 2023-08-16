pipeline {
    // master executor should be set to 0
    agent any
    tools {
          maven 'maven3'
          docker 'docker_my'
        }
    stages {
        stage('Build Jar') {
            steps {
                sh "mvn clean package -DskipTests"
            }
        }
        stage('Build Image') {
            steps {
                sh "docker build -t='heretic13/selenium-docker' ."
            }
        }
        stage('Push Image') {
            steps {
			    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'hardcore13', usernameVariable: 'dolbilov@gmail.com')]) {
			        sh "docker login --username=${user} --password=${pass}"
			        sh "docker push heretic13/selenium-docker:latest"
			    }
            }
        }
    }
}