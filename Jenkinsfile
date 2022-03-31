#!groovy

pipeline {
    agent any
    tools {
        jdk 'OpenJDK 11'
        maven 'Maven 3.8.5'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'mvn --version'
                script {
                    TAG_SELECTOR = readMavenPom().getVersion()
                }
                echo("TAG_SELECTOR=${TAG_SELECTOR}")
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
    post{
        always{
            slackSend channel: 'general'
        }
    }
}
