pipeline {
    agent {
        any {
            image 'maven:3.9.5-eclipse-temurin-21-alpine' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn clean package' 
                stash includes: 'target/*.jar', name: 'targetfiles'
                sh 'ls -al'
            }
        }
        stage('Deploy') { 
            steps {
                unstash 'targetfiles'
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
