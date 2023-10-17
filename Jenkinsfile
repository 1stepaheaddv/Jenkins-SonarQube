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
            sh '${mvnHome}/usr/bin/mvn -f WebApp/pom.xml sonar:sonar'
            }
        }

        stage ('Code Quality') {
        steps {
            withSonarQubeEnv('SonarQube') {
            sh 'mvn -f WebApp/pom.xml sonar:sonar'
            }
      }
    }

            stage ('Nexus upload') {
                steps {
                           nexusArtifactUploader artifacts: [[artifactId: 'WebApp', classifier: '', file: 'MyWebApp/target/MyWebApp.war', type: 'war']], credentialsId: '6ff32036-ec16-4226-9c57-b84ad15d96a5', groupId: 'com.dept.app', nexusUrl: 'ec2-18-221-32-13.us-east-2.compute.amazonaws.com:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT'

                }

            }

    }
}
