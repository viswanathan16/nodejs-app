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
                 def  dockerImage = docker.build("${env.DOCKER_IMAGE}:${env.BUILD_ID}")
  }
 }
}
 
       stage ('Test'){
           steps {
               script {
                   dockerImage.inside {
                        sh 'npm install'
                        sh 'npm test'
   }
  }
 }
}
  
       stage ('Deploy'){
           steps {
               script {
                   kubeconfig(credentialsId: 'kubeconfig', serverUrl: 'https://192.168.49.2:8443') {
                   sh 'kubectl apply -f kubernetes-deployment.yml'}

   }
  }
 }
}
       post {
           failure {
               emailext(
                    to: 'lunajavis05@gmail.com',
                    subject: "Pipeline Failed: ${env.JOB_NAME}:${env.BUILD_NUMBER}",
                    body: "Please check the Pipeline ASAP ${env.BUILD_URL}"
   ) 
  }
 } 
}            
