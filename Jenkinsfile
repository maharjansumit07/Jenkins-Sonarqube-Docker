pipeline {
  environment {
    repo = "maharjansumit07/jenkins_docker"
  }
  agent any
  stages {
    stage('Docker Build') {
      steps {
        sh 'docker build -t $repo:v$BUILD_NUMBER .'
      }
    }
    stage('Docker Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'Docker_Login', usernameVariable: 'User', passwordVariable: 'Password')]) {
          sh "docker login -u ${env.User} -p ${env.Password}"
          sh 'docker push $repo:v$BUILD_NUMBER'
        }
      }
    }
    stage('Clean docker image') {
      steps {
        sh 'docker rmi $repo:v$BUILD_NUMBER'
      }
    }
  }
}
