# docker-sample-repo
# Pipeline syntax#
pipeline {
    agent any

    stages {
        stage('Checking out the github code repo') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/praveenjram/docker-sample-repo.git']]])
            }
        }
        stage('Terraform init') {
            steps {
                sh ("terraform init");
            }
        }
        stage('Terraform action') {
            steps {
                echo "Terraform action from the parameter is ${action}"
                sh ("terraform ${action} --auto-approve");
            }
        }
        stage('Status') {
            steps {
                echo " Resouces has been deployed successfully"
                }
        }
       
    }
}
