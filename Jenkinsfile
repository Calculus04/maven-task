pipeline {
  agent any
  tools{
    maven 'sonarmaven'
  }
  environment {
    SONAR_TOKEN =credentials('sonar-token')
  }
stages{
  stage('Checkout'){
    steps{
      checkout scm
    }
  }
  stage('Build'){
    steps {
      bat 'mvn clean package'
    }
  }
  stage('SonarQube Analysis'){
    steps{
      withSonarQubeEnv('sonarqube'){
        bat"""
        mvn clean verify sonar:sonar \
  -Dsonar.projectKey=maven-demo \
  -Dsonar.projectName='maven-demo' \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=sqp_0c9456f834dafc357cc9a17bcae5d138c6d1ad90
        """
      }
    }
  }
}
  post {
    success {
      echo 'Pipeline completed successfully.'
    }
    failure{
      echo 'pipeline failed'
    }
  }
}
        
