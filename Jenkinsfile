#!groovy

tools {
    jdk 'OpenJDK 11'
}
pipeline {
    stages {
        stage('build') {
            steps {
                sh 'mvn --version'
                script {
                    TAG_SELECTOR = readMavenPom().getVersion()
                }
                echo("TAG_SELECTOR=${TAG_SELECTOR}")
            }
        }
    }
}
