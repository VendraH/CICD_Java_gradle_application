pipeline {
    // agent { label 'slave01' }
    agent any
    stages {
        stage('sonar quality check') {
            agent { 
                docker {
                    image 'gradle:6.7-jdk11'
                }
            }
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonarjenkins') {
                      sh 'chmod +x gradlew'
                      sh './gradlew sonarqube'
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


