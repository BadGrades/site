pipeline {
    agent any
    environment {
        BADGRADES_SECRET = credentials('badgrades-secret')
    }
    stages {
        stage('Test') {
            steps {
                sh "${tool name: 'sbt', type: 'org.jvnet.hudson.plugins.SbtPluginBuilder$SbtInstallation'}/bin/sbt test"
            }
        }
        stage('Build') {
            steps {
                sh "${tool name: 'sbt', type: 'org.jvnet.hudson.plugins.SbtPluginBuilder$SbtInstallation'}/bin/sbt docker:publishLocal"
            }
        }
        stage('Deploy') {
            agent {
                docker { image 'badgrades:1.0' }
            }
            steps {
                echo "I am inside a docker container!"
            }
        }
    }
}