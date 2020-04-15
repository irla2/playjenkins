pipeline {

  #environment {
  #  registry = "localhost:5000/new/html"
  #  dockerImage = ""
  #}

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/irla2/playjenkins.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker image build -t localhost:5000/html . + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
