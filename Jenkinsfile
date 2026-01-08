pipeline {
  agent {
    docker {
      image 'hashicorp/terraform:1.10.2'
      args '-u root'
    }
  }

  environment {
    TF_IN_AUTOMATION = 'true'
  }

  stages {
    stage('Terraform Init') {
      steps {
        sh 'terraform init -lockfile=readonly'
      }
    }

    stage('Terraform Plan') {
      steps {
        sh 'terraform plan'
      }
    }

    stage('Terraform Apply') {
      when {
        branch 'main'
      }
      steps {
        sh 'terraform apply -auto-approve'
      }
    }
  }
}