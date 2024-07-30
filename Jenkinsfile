pipeline {

    parameters {
        booleanParam(name: 'autoApprove', defaultValue: false, description: 'Automatically run apply after generating plan?')
    }
    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }

   agent  any
    stages {
        stage('checkout') {
            steps {
                 script{
                        dir("terraform")
                        {
                            git branch: 'main', url: 'https://github.com/adiattara/Jenkins-terraform.git'
                        }
                    }
                }
            }
        stage('Plan') {
                    steps {
                        sh 'pwd;cd terraform/ ; terraform init'
                        sh "pwd;cd terraform/ ; terraform plan -out tfplan"
                        sh 'pwd;cd terraform/ ; terraform show -no-color tfplan > tfplan.txt'
                    }
        }

    }

  }