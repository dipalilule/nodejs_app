pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
               //  git branch: 'master', credentialsId: 'gitcred', url: 'git@github.com:dipalilule/nodejs_app.git'
                git branch: 'master',
    credentialsId: 'gitcred',
    url: 'https://github.com/dipalilule/nodejs_app.git'
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
