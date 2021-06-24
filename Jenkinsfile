pipeline {
  environment {
<<<<<<< HEAD
    registry = "kamal0405/kamal0405/cicd-k8s-demo-html"
=======
    registry = "kamal0405/cicd-k8s-demo-html"
>>>>>>> 67ca1ea6e16f570525768db9e6300c6b6ab0bc6c
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
          docker.withRegistry('https://registry.hub.docker.com', 'docker_credentials') {
              dockerImage.push()
          }
        }
      }
    }
    stage('Deploy to Kubernetes'){
        steps{
<<<<<<< HEAD
          withKubeConfig([credentialsId: 'mykubeconfignew', serverUrl: '']) {
            powershell 'kubectl apply -f deployment.yaml'
=======
          script{    
            kubernetesDeploy(configs: "deployment.yaml", kubeconfigId: "mykubeconfignew")
          }  
>>>>>>> 67ca1ea6e16f570525768db9e6300c6b6ab0bc6c
       }
    }
  }
}