pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage("build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv(credentialsId:'39b2bc3a-5c97-4a81-971f-5e702336ec1a',installationName:'SQ-Docker') {
                sh 'mvn clean package sonar:sonar'
              }
            }
          }
          stage("Quality Gate") {
            steps {
              timeout(time: 10, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
              }
            }
          }      
    }
}
