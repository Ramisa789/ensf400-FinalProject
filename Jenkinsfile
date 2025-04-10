pipeline {
    agent any

    tools {
        jdk 'jdk11'
    }

    environment {
        GRADLE_OPTS = "-Dprojectname=ensf400-finalproject"
    }

    stages {
        stage('Build Container') {
        steps {
             sh 'sudo docker build -t finalproject-image .' 
        }
    }

        stage('Unit Tests') {
            steps {
                sh './gradlew test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('YourSonarQubeServer') {
                    withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                    sh "./gradlew sonarqube -Dsonar.login=$SONAR_TOKEN"
                    }
                }
            }
        }
    }
}
// test branch 3

