pipeline {
  agent any
  tools { 
        maven 'Maven'
        jdk 'Java'
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
      }
    }
   
    stage('push image to ECR'){
      steps {
       withDockerRegistry(credentialsId: 'ecr:us-east-1:aws-credentials', url: 'http://092390458462.dkr.ecr.us-west-2.amazonaws.com/address-service') {
          sh 'docker login -u AWS -p eyJwYXlsb2FkIjoiYlNPcDYxaFZ6Y1BLL1hoWkNxbm1aVlZIdGdFKy9IWVBiNWczb01qaUZJMGJYTXBPbGxPK3R5TEt5d0pZYkFMVzdGVzQyUzE1Q0VoYjRsQTVWTXRHemVETWJaS1BhU1hvMFJ1VjBSOXlScHRYbEM1Wmpwd0FmRHJFeEl6RHUvQWNtdTF4WlB5Yit6VUo0L1g4dU55dlp6c1N6SndaOWdOd3RlbXlOYS9rWVJCYnl4WjFmOHZqMGJSSjJQbXhVclkvamg1dlhSRGZHcTNtYjJGZmZObmlTbnRxcGFmT2QyQ2ZDbEU5b3dhZkoyc2NVb1RMa3pyY2w3UVBaUE1WNFBrZHMwTXN5NEFVMXdIb1RJS2Z6SktsUlZTTkZQOHBITzdpUFNxbHdFUmRsekR6MHRZMEtOVUVhdHBXQW5Ub3pjQTNXTVFLL3VLRXk2cEZJWlVidUJhR1NiZ2RQL21tVUJ4VmdMSUVGN1puMGNEK2hrNWkvWXhpTGxldnVUWjZzQ2c5a2xXSWk0bFlOUzlWMG54c1R6YVNtMStZUWF6ZWMvM1YzY2RYNzk5K1FNQWNSbXJrd25jSENMREdXMkM3YkVnSjFiRC9JVzh3UVVCdFA1dncvWE1EekJWVjl0bzRHUkg1aHFxanc5RmhiQ0lmKzNmV08yajFsVFhJSENhOWxTcFA2c1hQMDh5VlBBWVl6dXJSWnpTbkNHNU9wQzNRZVlvcW9QRDc2ZjFaVms4dS9PTk11OU9iNXBQT2pacUJSQ21TRnlkaGJSL1BSTVZyTmRONHJvTHFWOFl4K0t0RThOSHJXWUNvck5yQ0xIVHZXaERZQnNxY0V5cndGTjNyUHNOWDl6d1BiMml0UkRjaytRR3NHd24xN05TTnJaZ1Bnb3VEMUxGNGpKbDkrazJ1ZVpOOHVjenR1WUtpemJSTkd6SVB4SkFHWFNNdHdLR1U1WHVMLzc5UGF5aWhKS2V2ckUzMXl6eU1QYlNUaWx0amVlbVVNNTlCaGF3d3kzRnZhbzBPRmJwNFYweGJ4b1VST2dpL0JUZE1wdjB1THFzRkQxNmx6cWJ1MGl4dVQ5N0dYQkZlRnVBUmk2RU5PVkRWSmRGdXNBVHZheWJlT0h6TU9mYXNjUEkrWldoRWhKd3NHMm91L3g3NExBK0V6ckFMZDAvREo3N3hsVUllM1U0RXNndmp5ZnFwSXNSRi9pRjlodFBwWmZmaGtJRE5TS1Y0aytHS2NRNnVxejJtYVpuMUNFUEsxc3A0UlFlS1FjaVhteE51YUtSTG84aTB5dkJaVjgxNU5qbGVNRFpwb1pteU0za0JHNHQweHdhUTNIMDhCY3F3Nk1ER2x3ZlNCYTRkQVZtN0hmNXFuV0liSllCRm1Rd3VJZ3M5c3ljNUtSWnNlUENwajRqN2FtWFhUc0VndnBBTjVxQVlhZm5kM1dVaGU2bFc1aHNoamNCSVk2TGhhaUI3SW5EMmZjQzMiLCJkYXRha2V5IjoiQVFFQkFIajZsYzRYSUp3LzdsbjBIYzAwRE1lazZHRXhIQ2JZNFJJcFRNQ0k1OEluVXdBQUFINHdmQVlKS29aSWh2Y05BUWNHb0c4d2JRSUJBREJvQmdrcWhraUc5dzBCQndFd0hnWUpZSVpJQVdVREJBRXVNQkVFREMrZEREQ3QzL3gxYlRxcGxRSUJFSUE3ODVON3dlQnplcnllTjBab0JjRGZvZkE4cHhLMnVzb1RmbDJoYUhER2k2YVp5OFdla3ZYOFJQVkc5bnY1ZGNzYXRnM0V4dGNFK1ZzdUlwYz0iLCJ2ZXJzaW9uIjoiMiIsInR5cGUiOiJEQVRBX0tFWSIsImV4cGlyYXRpb24iOjE1NjM3NDcyMzN9 https://092390458462.dkr.ecr.us-west-2.amazonaws.com'
          sh 'docker tag address-service:latest 092390458462.dkr.ecr.us-west-2.amazonaws.com/address-service:latest'
          sh 'docker push 092390458462.dkr.ecr.us-west-2.amazonaws.com/address-service:latest'
        } 
      }
    }
  stage('deploy to ECR') {
      steps {
        node('eks-master-node'){
          checkout scm
         sh 'kubectl apply -f deployment.yaml' 
         sh 'kubectl apply -f service.yaml' 
        }
      }
    } 
  }
}
