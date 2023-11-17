pipeline {
    agent {
        docker {
            image 'maven:3.9.5-eclipse-temurin-21-alpine' 
            args '-v /tmp:/root/.m2'
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
