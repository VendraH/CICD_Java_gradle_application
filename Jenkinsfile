pipeline {
    // agent { label 'slave01' }
    agent any
    stages {
        stage('sonar quality check') {
            agent { 
                docker {
                    image 'openjdk:11'
                }
            }
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonartoken') {
                    // some block
                    sh 'chmod +x gradlew'
                    sh './gradlew sonarqube'
                    }
                }
            }
        }
    }
}


