pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'sbt universal:packageZipTarball'
            }
        }
        stage('Deploy') {
            steps {
                sh 'tar -xvzf target/universal/badgrades-1.0.tgz'
                sh 'badgrades-1.0/bin/badgrades -Dplay.http.secret.key=jahsdljkfp8bkbahsdigfjlb'
            }
        }
    }
}