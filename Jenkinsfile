pipeline {
    agent any

    tools {
        // Install the Maven version needed
        maven 'mvn'
        jdk 'JDK 11'
    }

    environment {
        // Define SonarQube server
        SONARQUBE_SERVER = 'SonarQube-Server'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository
                git url: 'https://github.com/errachidy10/simplePourTesteJenkinsEtSonarQube.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                // Build the project using Maven
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            environment {
                // Define SonarQube authentication
                SONAR_AUTH_TOKEN = credentials('sonarJenkinsToken1')
            }
            steps {
                // Run SonarQube analysis
                sh 'mvn sonar:sonar -Dsonar.projectKey=simplePourTesteJenkinsEtSonarQube -Dsonar.host.url=$SONARQUBE_SERVER -Dsonar.login=$SONAR_AUTH_TOKEN'
            }
        }

        stage('Test') {
            steps {
                // Run tests
                sh 'mvn test'
            }
        }
    }

    post {
        always {
            // Archive the build artifacts
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            // Publish test results
            junit '**/target/surefire-reports/*.xml'
        }
    }
}