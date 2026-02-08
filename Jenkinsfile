pipeline {
  agent any

  stages {

    stage('Checkout GitHub repo') {
      steps {
        git branch: 'main',
            url: 'https://github.com/Juanita456/helloDockerEvaluacion.git'
      }
    }

    stage('Build and Tag Docker Image') {
      steps {
        sh 'docker build -t hellodocker .'
        sh 'docker tag hellodocker soul433/hellodocker:latest'
      }
    }

    stage('Push Docker Image to Docker Hub') {
      steps {
        withCredentials([string(credentialsId: 'docker_hub', variable: 'DOCKER_PWD')]) {
          sh 'echo $DOCKER_PWD | docker login -u soul433 --password-stdin'
          sh 'docker push soul433/hellodocker:latest'
        }
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        kubeconfig(credentialsId: 'kubeconfig', serverUrl: '') {
    sh 'kubectl apply -f deploymentsvc.yaml'
}
      }
    }
  }
}
