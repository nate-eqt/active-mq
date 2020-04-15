pipeline {
    agent any
    stages {
        stage("build & SonarQube analysis") {
            steps {
              withSonarQubeEnv(installationName:'Docker-SQ') {
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
