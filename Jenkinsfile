pipeline {
    agent any
    environment {
        BADGRADES_SECRET = credentials('badgrades-secret')
    }
    stages {
        stage('Build') {
            steps {
                sh "${tool name: 'sbt', type: 'org.jvnet.hudson.plugins.SbtPluginBuilder$SbtInstallation'}/bin/sbt universal:packageZipTarball"
            }
        }
        stage('Deploy') {
            steps {
                echo "Using ${env.BADGRADES_SECRET) for badgrades-site play application secret"
                sh 'tar -xvzf target/universal/badgrades-1.0.tgz'
                sh "nohup badgrades-1.0/bin/badgrades -Dplay.http.secret.key=${env.BADGRADES_SECRET} &"
            }
        }
    }
}
