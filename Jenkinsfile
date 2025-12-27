pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('Docker')
    }
    stages { 
        stage('Git Checkout') {
            steps{
            git 'https://github.com/bishal1289/CICD_Pipline_To_Integrate_Jenkins_With_Docker'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t bishal1289/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push bishal1289/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

