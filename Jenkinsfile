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
                    GIT_TAG = getArtefactVersionFromLastCommitTag()
                }
                echo("TAG_SELECTOR=${TAG_SELECTOR}")
                echo("GIT_TAG_SELECTOR=${GIT_TAG}")
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
            slackSend channel: 'general' , message: 'please check the pipeline status'
        }
    }
}
def getArtefactVersionFromLastCommitTag() {
    version = sh script: "git describe --abbrev=0 | sed -E 's/^v(.*)/\\1/g' | tr -d '\\n'", returnStdout: true
    return version
}
