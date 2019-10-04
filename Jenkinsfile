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
    
    stage('Create RDS') {
      steps {
        withAWS(region:'us-west-2', credentials:'aws-final') {
          sh 'aws cloudformation create-stack --stack-name rds --template-body file:///root/ekscluster/rds.yml --region us-west-2'
        }          
      }
    }
      
    stage('Get RDS Endpoint') {
      steps {
        withAWS(region:'us-west-2', credentials:'aws-final') {
          sh 'aws cloudformation describe-stacks --stack-name rds --query Stacks[0].Outputs[0].OutputValue > /tmp/rds-endpoint.txt'
        }
      }
    }      
    
  }
}
