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
            sh 'docker build -t finalproject-image .'  
            sh 'docker tag finalproject-image hannagracec/ensf400-finalproject:v1'  
            sh 'docker push hannagracec/ensf400-finalproject:v1'  
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

