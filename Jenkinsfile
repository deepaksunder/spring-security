pipeline {
    agent any

    tools {
        maven 'Maven_3.9.11'   // must match the name in Global Tool Config
        jdk 'Java_21'         // must match the name in Global Tool Config
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/deepaksunder/spring-security.git', branch: 'master'
            }
        }

        stage('Build') {
            steps {
                dir('spring-security') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage('Test') {
            steps {
                dir('spring-security') {
                    sh 'mvn test'
                }
            }
            post {
                always {
                    junit 'spring-security/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                dir('spring-security') {
                    sh 'mvn package'
                }
            }
            post {
                success {
                    archiveArtifacts artifacts: 'spring-security/target/*.jar', fingerprint: true
                }
            }
        }
    }
}
