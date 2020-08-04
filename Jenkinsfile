pipeline {
  agent any
  tools { 
        maven 'Maven'
        jdk 'JAVA_HOME'
  }
  stages {
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace... */
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
        sh 'echo $USER'
        sh 'echo whoami'
      }
    }
    stage('Docker Build') {
      steps {
        sh '/usr/bin/docker build -t address-service .'
        sh 'echo build finished'
      }
    }
   
    stage('push image to ECR'){
      steps {
        sh 'echo entered ecr'
       withDockerRegistry(credentialsId: 'ecr:us-east-1:aws-cred', url: 'http://349229500297.dkr.ecr.us-east-1.amazonaws.com/address-service') {
          sh 'docker tag address-service:latest 349229500297.dkr.ecr.us-east-1.amazonaws.com/address-service:latest'
          sh 'docker push 349229500297.dkr.ecr.us-east-1.amazonaws.com/address-service:latest'
        } 
      }
    }
  stage('deploy to ECR') {
      steps {
         sh 'curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.17.7/2020-07-08/bin/linux/amd64/kubectl

         sh 'curl -o kubectl.sha256 https://amazon-eks.s3.us-west-2.amazonaws.com/1.17.7/2020-07-08/bin/linux/amd64/kubectl.sha256'

         sh 'openssl sha1 -sha256 kubectl'

         sh 'chmod +x ./kubectl'

         sh 'cp ./kubectl $HOME/bin/kubectl && export PATH=$HOME/bin:$PATH'

         sh 'echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc'

         sh 'kubectl version --short --client'
         sh 'kubectl apply -f deployment.yaml' 
         sh 'kubectl apply -f service.yaml'  
      }
    } 
  }
}
