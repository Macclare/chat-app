pipeline {
    agent any

    environment {
        SSH_CREDENTIALS_ID = 'ansible-key'
        REMOTE_USER = 'ec2-user'
        REMOTE_HOST = '13.50.149.174'
        PLAYBOOK_PATH = '/var/www/html/chat-app/ansible/setup.yml'
    }

    stages {
        stage('Pull latest code') {
            steps {
                git branch: 'dev', url: 'https://github.com/Macclare/chat-app.git'
            }
        }

        stage('Run Ansible Playbook on EC2') {
            steps {
                sshagent(credentials: [env.SSH_CREDENTIALS_ID]) {
                    sh """
                        ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${REMOTE_HOST} \
                        'ansible-playbook ${PLAYBOOK_PATH}'
                    """
                }
            }
        }
    }
}
