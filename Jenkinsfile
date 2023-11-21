pipeline {
    agent {
        any {
            image 'maven:3.9.5-eclipse-temurin-21-alpine' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn clean package deploy --s settings.xml' 
                stash includes: 'target/*.jar', name: 'targetfiles'
            }
        }
        stage('Sonar') { 
            steps {
                
                sh 'mvn sonar:sonar \
                    -Dsonar.projectKey=test \
                    -Dsonar.host.url=http://127.0.0.1:8084 \
                    -Dsonar.login=e75743a5d9970795d00d7132ed779d462ddbfd06'
            }
        }     
        stage('Deploy') { 
            steps {
                unstash 'targetfiles'
                sh 'java -jar target/spring-boot-0.0.2-SNAPSHOT.jar'
            }
        }   
    }
    post {
        // Clean after build
        always {
            cleanWs(cleanWhenNotBuilt: false,
                    deleteDirs: true,
                    disableDeferredWipeout: true,
                    notFailBuild: true,
                    patterns: [[pattern: '.gitignore', type: 'INCLUDE'],
                               [pattern: '.propsfile', type: 'EXCLUDE']])
        }
    }
}
