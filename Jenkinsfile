pipeline {
    agent any
    tools {
          maven 'maven3'
          dockerTool 'docker3'
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
			    withCredentials([usernamePassword(credentialsId: 'docker_hub', passwordVariable: 'pass', usernameVariable: 'user')]) {
			        sh "docker login --username=${user} --password=${pass}"
			        sh "docker push heretic13/selenium-docker:latest"
			    }
            }
        }
    }
}