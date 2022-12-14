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
                    sh 'chmod +x gradlew'
                    sh './gradlew sonarqube -Dsonar.projectKey=test -Dsonar.host.url=http://20.198.76.175:9000 -Dsonar.login=sonartoken'
                    }
                }
            }
        }
    }
}


