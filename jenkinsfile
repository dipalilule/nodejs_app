pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                git credentialsId: 'gitcred',
                url: 'git@github.com:dipalilule/nodejs_app.git'
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
