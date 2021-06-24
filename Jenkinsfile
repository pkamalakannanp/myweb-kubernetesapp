pipeline {
  environment {
    registry = "kamal0405/test-html-cicd"
    registryCredential = 'docker_credentials'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Checkout Source') {
      steps {
        git 'https://github.com/pkamalakannanp/myweb-kubernetesapp.git'
      }
    }
    stage('Building Docker Image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Push Image To Docker Hub') {
      steps{
        script {
          /* Finally, we'll push the image with two tags:
                   * First, the incremental build number from Jenkins
                   * Second, the 'latest' tag.
                   * Pushing multiple tags is cheap, as all the layers are reused. */
          docker.withRegistry('https://registry.hub.docker.com', 'docker_redentials') {
              dockerImage.push("${env.BUILD_NUMBER}")
              dockerImage.push("latest")
          }
        }
      }
    }
    stage('Deploy to Kubernetes'){
        steps{
          withKubeConfig([credentialsId: 'mykubeconfignew', serverUrl: '']) {
            powershell 'kubectl apply -f deployment.yaml'
          }
       }
    }
  }
}