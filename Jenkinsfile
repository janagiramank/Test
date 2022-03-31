#!groovy

pipeline {
    agent { label 'jenkins-java-docker' }

    tools {
        jdk 'OpenJDK 11'
    }


    stages {
        stage("Tests & Package") {
            steps {
                checkout scm
                sh "mvn clean verify"
                sh "mvn --batch-mode -U deploy"
                script {
                    TAG_SELECTOR = readMavenPom().getVersion()
                }
                echo("TAG_SELECTOR=${TAG_SELECTOR}")
            }
        }

    }
}