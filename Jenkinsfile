
pipeline {
  agent any
  stages {
    
    stage('Create EKS Cluster') {
      steps {
        withAWS(region:'us-west-2', credentials:'aws-final') {
          eksctl create cluster \
          --name ekscluster \
          --version 1.14 \
          --nodegroup-name standard-workers \
          --node-type t3.medium \
          --nodes 1 \
          --nodes-min 1 \
          --nodes-max 2 \
          --node-ami auto
        }
      }
    }
    
  }
}
