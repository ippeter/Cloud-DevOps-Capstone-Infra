
pipeline {
  agent any
  
  stages {
    
    stage('Create EKS Cluster') {
      steps {
        withAWS(region:'us-west-2', credentials:'aws-final') {
          sh 'eksctl create cluster --name capstonecluster --version 1.14 --nodegroup-name standard-workers --node-type t3.medium --nodes 1 --nodes-min 1 --nodes-max 2 --node-ami auto'
        }
      }
    }
    
    stage('Create kubectl Configuration') {
      steps {
        withAWS(region:'us-west-2', credentials:'aws-final') {
          sh 'aws eks update-kubeconfig --name capstonecluster'
        }
      }
    }
    
    stage('Get Deployments') {
      steps {
        withAWS(region:'us-west-2', credentials:'aws-final') {
          sh 'kubectl get deployment'
        }
      }
    }
    
  }
}
