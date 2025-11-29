pipeline {
    agent any

    environment {
        WORKSPACE_PATH = "${env.WORKSPACE}"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/skfarid45/Ansible-Project.git'
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy using Ansible') {
            steps {
                sh """
                   ansible-playbook ansible/deploy.yml \
                   -i ansible/inventory \
                   --extra-vars 'workspace=${WORKSPACE_PATH}'
                """
            }
        }
    }
}

