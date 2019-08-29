pipeline {
    agent any
    stages {
        stage ('Checkout') {
            steps {
                git branch: 'master', url: '/vagrant/vagrant-jenkins-docker'
            }
        }
        stage('Git log') {
            steps {
                sh 'git status'
                sh 'git log -n 5'
            }
        }
   }
}