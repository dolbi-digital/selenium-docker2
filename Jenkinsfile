pipeline {
    // master executor should be set to 0
    agent any
    stages {
        stage('Build Jar') {
            steps {
                bat "mvn clean package -DskipTests"
            }
        }
        stage('Build Image') {
            steps {
                bat "docker build -t='heretic13/docker' ."
            }
        }
        stage('Push Image') {
            steps {
			    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'hardcore13', usernameVariable: 'heretic13')]) {
                    //sh
			        bat "docker login --username=${user} --password=${pass}"
			        bat "docker push heretic13/docker:latest"
			    }
            }
        }
    }
}