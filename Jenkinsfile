pipeline {
    agent { label 'slave-amar' }
    environment {
    DOCKERHUB_CREDENTIALS = credentials('AmarDockerToken')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/AmardeepSambaru/nodejs-demo-pipelineproject.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t amardeepsambaru/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u amardeepsambaru --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push amardeepsambaru/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

