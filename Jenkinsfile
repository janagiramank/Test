#!groovy

pipeline {
    agent any
    tools {
        jdk 'OpenJDK 11'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
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
}
