pipeline {
    agent any
    environment {
       DOCKER_IMAGE = "nodejs-app"
}
    stages {
       stage ('Checkout') {
          steps {
              checkout scm
 }
} 
       stage ('Build') {
          steps {
             script {
                 dockerImage = dokcer.build("${env.DOCKER_IMAGE}:${env.BUILD_ID}")
  }
 }
}
 
       stage ('Test'){
           steps {
               script {
                   dockerImage.inside {
                        sh 'chmod +x node_modules/.bin/mocha'
                        sh 'npm test'
  }
 }
}
  
       stage ('Deploy')
           steps {
               script {
                   kubeconfig(credentialsId: 'kubeconfig', serverurl: https://127.0.0.1:32769') {
                   sh 'kubectl apply -f kubernetes-deployment.yml'
}


    }
   }
  }
 }
}            
