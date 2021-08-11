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
        stage('docker build') {
            steps {
               docker build --no-cache -t 589606845106.dkr.ecr.us-east-1.amazonaws.com/nodejs-image-demo:$BUILD_NUMBER .
               aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 589606845106.dkr.ecr.us-east-1.amazonaws.com
               docker push 589606845106.dkr.ecr.us-east-1.amazonaws.com/frontenduat:$BUILD_NUMBER
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
