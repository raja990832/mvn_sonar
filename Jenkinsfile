pipeline {
   agent any
    stages {
      stage('Git Checkout') {
         steps {           
            git url: 'https://github.com/raja990832/mvn_sonar.git'
        }
    }
    stage('Build Analysis') {
        steps {
            withSonarQubeEnv('sonar') {
                sh '/opt/maven/bin/mvn clean verify sonar:sonar -Dsonar.password=admin -Dsonar.login=admin -Dmaven.test.skip=true'
            }
        }
    }
    stage("Quality Gate") {
            steps {
              timeout(time: 2, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
    stage ('Deploy') {
        steps {
            sh '/opt/maven/bin/mvn clean install'
        }
    }
   
}
}
