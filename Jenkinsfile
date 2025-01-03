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
      bat 'mvn clean verify'
    }
  }
  stage('SonarQube Analysis'){
    steps{
      withSonarQubeEnv('sonarqube'){
        bat """
        mvn clean verify sonar:sonar \
  -Dsonar.projectKey=maven \
  -Dsonar.projectName='maven' \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=sqp_58fb79d071b54f8a310dd456bdebf885fbc2bf8f \
  -Dsonar.coverage.jacoco.xmlReportPaths=target/site/jacoco/jacoco.xml \
  -Dsonar.pmd.reportPaths=target/pmd.xml
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
        
