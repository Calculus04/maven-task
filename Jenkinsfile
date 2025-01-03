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
  -Dsonar.sources=src/main/java \
  -Dsonar.tests=src/test/java \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=sqp_58fb79d071b54f8a310dd456bdebf885fbc2bf8f \
  -Dsonar.junit.reportPaths=target/surefire-reports \
  -Dsonar.jacoco.reportPaths=target/site/jacoco/jacoco.xml \
  -Dsonar.pmd.reportPaths=target/pmd-duplicates.xml \
  -Dsonar.login=%SONAR_TOKEN%
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
        
