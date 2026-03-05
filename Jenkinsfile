pipeline {
    agent any
    stages {
        stage('Build'){
            steps {
                 echo 'building and tagging for dockerhub..'
                sh 'docker build -t myapp:${BUILD_NUMBER} .'
                sh 'docker tag myapp:${BUILD_NUMBER} noakhali99/myapp:${BUILD_NUMBER}'

            }
        }
        stage('push to dockerhub'){
            steps {
              
              echo 'pushing to dockerhub..'

                    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'password', usernameVariable: 'uname')]) {
                    sh 'docker login -u $uname -p $password'
                    sh 'docker push noakhali99/myapp:${env.BUILD_NUMBER}'
                    sh 'docker logout'
                    }
            }
        }
    }
}