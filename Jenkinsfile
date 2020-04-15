pipeline {

  ##environment {
  ##  registry = "localhost:5000/new/html"
  ##  dockerImage = ""
  ##}

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
          docker image build -t localhost:5000/html:1.0 .
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker push localhost:5000/html:1.0 
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
