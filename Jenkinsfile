pipeline {
    agent any

    tools {
        jdk 'java'
        maven 'apache-maven'
        git 'Git'
    }

    environment {
        WORKSPACE_PATH = "${env.WORKSPACE}"
        WAR_NAME = "Farid-Ansible.war"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/skfarid45/Ansible-Project.git'
            }
        }

        stage('Build WAR') {
            steps {
                sh "mvn clean package -DskipTests"
                echo "WAR built: target/${WAR_NAME}"
            }
        }

        stage('Deploy using Ansible') {
            steps {
                sh """
                    ansible-playbook ansible/deploy.yml \
                    -i ansible/inventory \
                    --private-key=/var/lib/jenkins/.ssh/farid.pem \
                    --extra-vars "workspace=${WORKSPACE_PATH} war_name=${WAR_NAME}"
                """
            }
        }
    }

    post {
        success {
            echo "Deployment Completed Successfully!"
        }
        failure {
            echo "Deployment Failed!"
        }
    }
}
