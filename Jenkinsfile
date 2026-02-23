pipeline {
    agent any

    triggers {
        cron('H/5 * * * 1')
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvnw.cmd clean compile'
            }
        }

        stage('Test') {
            steps {
                bat 'mvnw.cmd test'
            }
        }

        stage('Code Coverage - JaCoCo') {
            steps {
                bat 'mvnw.cmd jacoco:report'
            }
        }

        stage('Package Artifact') {
            steps {
                bat 'mvnw.cmd package -DskipTests'
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
        }
    }
}