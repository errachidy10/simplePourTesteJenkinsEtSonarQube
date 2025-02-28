pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/errachidy10/simplePourTesteJenkinsEtSonarQube.git'
            }
        }
        stage('Build') {
            steps {
                // Add your build steps here (e.g., Maven, Gradle commands)
                // Example (Maven):
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                // Assumes your tests generate reports in the "target/surefire-reports" directory
                junit 'target/surefire-reports/*.xml'  // Adjust the path if necessary
            }
        }
        stage('SonarQube Analysis') {
           steps {
             // Add SonarQube analysis steps here (after the build and test stages)
           }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true // Change to your output artifact(s)
        }
    }
}