pipeline {
    agent any
    stages {
        stage('Build'){
            steps {
                 echo 'building and tagging for dockerhub..'
                docker build -t myapp:{{env.BUILD_NUMBER}} .
                docker tag myapp:{{env.BUILD_NUMBER}} noakhali99/myapp:{{env.BUILD_NUMBER}}

            }
        }
        stage('push to dockerhub'){
            steps {
              
              echo 'pushing to dockerhub..'

                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'password', usernameVariable: 'uname')]) {
    // some block

                sh 'docker login -u $uname -p $password'
                sh 'docker push noakhali99/myapp:{{env.BUILD_NUMBER}}'
                sh 'docker logout'
                }
            }
        }
    }
}