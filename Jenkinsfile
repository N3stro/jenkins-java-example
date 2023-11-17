pipeline {
    agent {
        any {
            image 'maven:3.9.5-eclipse-temurin-21-alpine' 
        }
    }
    triggers {
        pollSCM('* * * * *') // Poll SCM every minute
    }
    stages {
        stage('Build') { 
            steps {
                script {
                    if (changeset.isEmpty()) {
                        echo 'No changes in the main branch. Skipping build.'
                        currentBuild.result = 'ABORTED'
                    } else {
                        echo 'Building with changes in the main branch.'
                        sh 'mvn -B clean package'
                    }
                }
            }
        }
        stage('Deploy') { 
            steps {
                sh './mvnw spring-boot:run'
            }
        }
    }
}
