pipeline {
    agent {
        any {
            image 'maven:3.9.5-eclipse-temurin-21-alpine' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B clean package' 
            }
        }
        stage('Deploy') { 
            steps {
                sh './mvnw spring-boot:run'
            }
        }
    }
}
