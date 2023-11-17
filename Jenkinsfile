pipeline {
    agent {
        docker {
            image 'maven:3.9.5-eclipse-temurin-21-alpine' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh './mvnw spring-boot:run' 
            }
        }
    }
}