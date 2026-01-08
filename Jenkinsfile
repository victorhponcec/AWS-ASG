pipeline {
  agent any

  environment {
    WORKDIR = "/workspace/my-terraform-project"
  }

  stages {
    stage('Checkout') {
      steps {
        sh '''
          mkdir -p $WORKDIR
          git clone https://github.com/you/terraform-repo.git $WORKDIR
        '''
      }
    }

    stage('Terraform Init') {
      steps {
        sh '''
          docker exec terraform sh -c "
            cd $WORKDIR &&
            terraform init
          "
        '''
      }
    }

    stage('Terraform Plan') {
      steps {
        sh '''
          docker exec terraform sh -c "
            cd $WORKDIR &&
            terraform plan
          "
        '''
      }
    }

    stage('Terraform Apply') {
      when { branch 'main' }
      steps {
        sh '''
          docker exec terraform sh -c "
            cd $WORKDIR &&
            terraform apply -auto-approve
          "
        '''
      }
    }
  }
}