pipeline {
  environment {
    registry = "kamal0405/cicd-k8s-demo-html"
    registryCredential = 'docker_credentials'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Checkout Source') {
      steps {
        git 'https://github.com/pkamalakannanp/myweb-kubernetesapp'
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
          script    
            kubernetesDeploy(configs: "deployment.yml", kubeconfigId: "mykubeconfignew")
       }
    }
  }
}