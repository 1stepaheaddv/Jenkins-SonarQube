pipeline {
    agent any

    tools {
     maven '/opt/maven'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '1stepaheaddv', url: 'https://github.com/1stepaheaddv/Jenkins-SonarQube.git']])
            }
        }

       stage ('Build') {
         steps {
              sh 'mvn clean install -f WebApp/pom.xml'
            }
        }

        stage ('Code Quality') {
        steps {
            withSonarQubeEnv('SonarQube') {
            sh 'mvn -f WebApp/pom.xml sonar:sonar'
            }
      }
    }
}
}   
