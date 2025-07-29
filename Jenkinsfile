pipeline {
    agent any

    tools {
        maven 'Maven3' // Ensure Maven3 is configured under Jenkins > Global Tool Configuration
    }

    environment {
        SONARQUBE = 'SonarQubeServer' // Name must match Jenkins > Manage Jenkins > Configure System > SonarQube section
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'ganesh.developer', url: 'https://github.com/ganeshsp2296/assignment_29_07.git'
            }
        }

        stage('SonarQube Code Scan') {
            steps {
                withSonarQubeEnv("${SONARQUBE}") {
                    sh """
                        mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=assignment-29-07 \
                        -Dsonar.host.url=http://sonarqube-service:9000
                    """
                }
            }
        }

        stage('Build Artifacts') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Verify Artifact') {
            steps {
                sh 'ls -lh target/*.jar || echo "No artifact found!"'
            }
        }
    }
}
