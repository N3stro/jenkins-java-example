pipeline {
    agent {
        docker {
            image 'maven:3.9.5-eclipse-temurin-17-alpine' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
    }
}
