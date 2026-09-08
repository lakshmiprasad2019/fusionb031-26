pipeline {
    agent any

    parameters {
        choice(
            name: 'ACTION',
            choices: ['apply', 'destroy'],
            description: 'Select whether to apply infrastructure changes or destroy existing resources.'
        )
    }


    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/lakshmiprasad2019/fusionb031-26.git'
            }
        }

        stage('Terraform Init') {
            steps {
                    sh 'terraform init'
                }
            }
        

        stage('Terraform Plan') {
            steps {
                    script {
                        if (params.ACTION == 'destroy') {
                            sh 'terraform plan -destroy'
                        } else {
                            sh 'terraform plan'
                        }
                }
            }
        }

        stage('Terraform Execution') {
            steps {
                    script {
                        if (params.ACTION == 'destroy') {
                            sh 'terraform destroy -auto-approve'
                        } else {
                            sh 'terraform apply -auto-approve'
                        }
                    }
            }
        }
    }
}

