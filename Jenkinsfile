pipeline {
    agent any

    environment {
        SSH_CREDENTIALS_ID = 'ansible-key'
        INVENTORY_PATH = 'ansible/inventory.ini'
        PLAYBOOK_PATH = 'ansible/setup.yml'
    }

    stages {
        stage('Pull latest code') {
            steps {
                git branch: 'dev', url: 'https://github.com/Macclare/chat-app.git'
            }
        }

        stage('Run Ansible Playbook from Jenkins') {
            steps {
                sshagent(credentials: [env.SSH_CREDENTIALS_ID]) {
                    sh """
                        ansible-playbook -i ${INVENTORY_PATH} ${PLAYBOOK_PATH}
                    """
                }
            }
        }
    }
}
