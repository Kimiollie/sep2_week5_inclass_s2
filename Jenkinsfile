pipeline {
    agent any

    tools {
            maven 'maven'
        }

    environment {
        SONARQUBE_SERVER = 'SonarQubeServer'  // The name of the SonarQube server configured in Jenkins
        SONAR_TOKEN = 'sqa_4ffde795273bb1703f0e916f9162f8abb20c34fb' // Store the token securely
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Kimiollie/sep2_week5_inclass_s2.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQubeServer') {
                    sh """
                        sonar-scanner \
                            -Dsonar.projectKey=devops-demo \
                            -Dsonar.sources=src \
                            -Dsonar.projectName=DevOps-Demo \
                            -Dsonar.host.url=http://localhost:9000 \
                            -Dsonar.login=${env.SONAR_TOKEN} \
                            -Dsonar.java.binaries=target/classes
                    """
                }
            }
        }

    }
}
