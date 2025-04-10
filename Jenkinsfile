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
            }
        }

        stage('Unit Tests') {
            steps {
                catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                    sh './gradlew test'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                    withSonarQubeEnv('YourSonarQubeServer') {
                        withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                            sh "./gradlew sonarqube -Dsonar.login=$SONAR_TOKEN"
                        }
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }

        success {
            echo 'Pipeline succeeded.'
        }

        failure {
            echo 'Pipeline failed.'
        }
    }
}
