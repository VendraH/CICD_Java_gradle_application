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
                      sh './gradlew sonarqube --status'
                    }
                    
                    timeout(time: 1, unit: 'HOURS') {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      }
                    }
                }
            }
        }
    }
}


