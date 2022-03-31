#!groovy

pipeline {
    agent any
    tools {
        jdk 'OpenJDK 11'
    }
    environment {
        // If your using the official maven image, these are probably where it puts it
        MAVEN_HOME = 'usr/local/maven'
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
}
