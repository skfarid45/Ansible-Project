pipeline {
    agent any

    tools {
        jdk 'java'
        maven 'apache-maven'
        git 'Git'
    }

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
                sh "mvn clean package"
            }
        }

        stage('Deploy to Tomcat using Ansible') {
            steps {
                sh """
                   ansible-playbook ansible/deploy.yml \
                   -i ansible/inventory \
                   --private-key=/var/lib/jenkins/.ssh/farid.pem \
                   --extra-vars "workspace=${WORKSPACE_PATH}"
                """
            }
        }
    }
}

