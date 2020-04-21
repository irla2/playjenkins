pipeline {

  agent { label 'kubepod' }

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/irla2/playjenkins.git', branch:'master'
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "nginx.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}

