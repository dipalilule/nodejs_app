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
                sh """
               docker build --no-cache -t 595552316002.dkr.ecr.ap-south-1.amazonaws.com/nodejs-image-demo:$BUILD_NUMBER .
               aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 595552316002.dkr.ecr.ap-south-1.amazonaws.com
               docker push 595552316002.dkr.ecr.ap-south-1.amazonaws.com/nodejs-image-demo:$BUILD_NUMBER
               """
            }
        }
        stage('Deploy') {
            steps {
                 sh """
               
                 docker pull 595552316002.dkr.ecr.ap-south-1.amazonaws.com/nodejs-image-demo:$BUILD_NUMBER
                 docker run -p 8000:8081 -d 595552316002.dkr.ecr.ap-south-1.amazonaws.com/nodejs-image-demo:$BUILD_NUMBER
                 TASK_DEFINITION_FE_UAT=$(aws ecs describe-task-definition --task-definition "$TASK_FAMILY_FE_UAT" --region "ap-south-1")
                 NEW_TASK_DEFINTIION_FE_UAT=$(echo $TASK_DEFINITION_FE_UAT | jq --arg IMAGE "$NEW_IMAGE_FE_UAT" '.taskDefinition | .containerDefinitions[0].image = $IMAGE | del(.taskDefinitionArn) | del(.revision) | del(.status) | del(.requiresAttributes) | del(.compatibilities)')
                 aws ecs register-task-definition --region "ap-south-1" --cli-input-json "$NEW_TASK_DEFINTIION_FE_UAT"

              """
              


            }
        }
    }
}
