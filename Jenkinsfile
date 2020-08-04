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
       withDockerRegistry(credentialsId: 'ecr:us-east-1:aws-cred', url: 'http://919088956184.dkr.ecr.us-east-1.amazonaws.com/address-service') {
          sh 'docker tag address-service:latest 919088956184.dkr.ecr.us-east-1.amazonaws.com/address-service:latest'
          sh 'docker push 919088956184.dkr.ecr.us-east-1.amazonaws.com/address-service:latest'
        } 
      }
    }
  stage('deploy to ECR') {
      steps {
         sh 'kubectl apply -f deployment.yaml' 
         sh 'kubectl apply -f service.yaml'  
      }
    } 
  }
}
