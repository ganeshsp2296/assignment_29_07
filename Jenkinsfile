pipeline {
    agent any

    tools {
        maven 'Maven3'               // Make sure Maven3 is configured under Global Tools
        sonarQubeScanner 'SonarScanner'  // Optional if using mvn plugin, but safe to add
    }

    environment {
        SONARQUBE = 'SonarQubeServer'  // Must match Jenkins > Configure System > SonarQube server name
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
                    sh '''
                        mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=assignment-29-07 \
                        -Dsonar.projectName=assignment-29-07 \
                        -Dsonar.host.url=http://sonarqube-service:9000 \
                        -Dsonar.login=admin
                    '''
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
