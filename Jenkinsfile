pipeline {
      agent {
        docker {
            image 'docker:latest' // Use a imagem Docker que contém o Docker CLI
        }
    }

  stages {
    stage('Build Docker Image'){
      steps {
        script {
          dockerapp = docker.build("cjanderson/guia-jenkins:${env.BUILD_ID}", './src')     
        }
      }
    }

    stage('Push Docker Image'){
      steps {
        script {
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub'){
                dockerapp.push('latest')
                dockerapp.push("${env.BUILD_ID}") 
            }
        }
      }
    }
    stage('Deploy no Kubernetes'){
      steps {
        sh 'echo "Executando o comando kubectl apply"'
      }
    }
  }
}
