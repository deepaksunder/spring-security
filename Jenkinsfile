pipeline {
    agent any

    tools {
        maven 'Maven_3.9.6'   // Ensure Maven is configured in Jenkins
        jdk 'Java_21'     // Ensure JDK is configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/deepaksunder/spring-security.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                sh 'java -jar target/your-app.jar'
            }
        }
    }
}
