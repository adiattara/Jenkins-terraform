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
        stage('Terraform Plan') {
                    steps {
                        script {
                            withCredentials([aws(credentialsId: 'awsFoo', accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                            secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                                sh '''
                                    cd terraform
                                    terraform plan -out=tfplan
                                '''
                            }
                        }
                    }
        }


    }

}