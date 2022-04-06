#!groovy

pipeline {
    agent any
    tools {
        jdk 'OpenJDK 11'
        maven 'Maven 3.8.5'
    }

    stages {
//        stage('Checkout') {
//            steps {
//                scmSkip(deleteBuild: true, skipPattern:'.*\\[ci skip\\].*')
//            }
//        }
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'mvn --version'
                script {
                   // withCredentials([sshUserPrivateKey(credentialsId: 'git-ssh')]) {
                        sh "git config --global --add user.name janagiramank"
                        sh "git config --global --add user.email k.janagiraman@elsevier.com"
                        version = sh(returnStdout: true, script: "mvn help:evaluate -Dexpression=project.version -q -DforceStdout").trim()
                        sh "git checkout main"
                        sh "git reset --hard origin/main"
                        sh "git branch --set-upstream-to=origin/main main"
                        sh "git pull"
                        sh "mvn -B gitflow:release -Drevision=${version.replaceAll("-SNAPSHOT","")}"
                   // }

                    //GIT_TAG = getArtefactVersionFromLastCommitTag()
                }
                //echo("GIT_TAG_SELECTOR=${GIT_TAG}")
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
