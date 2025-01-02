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
        bat """
        mvn clean verify sonar:sonar \
  -Dsonar.projectKey=maven-task\
  -Dsonar.projectName='maven task'\
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=sqp_a8c80683d49c849f9ea3f39b8d1afee116fba34c
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
        
