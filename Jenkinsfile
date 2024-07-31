pipeline {
    agent any
    environment {
        ANSIBLE_PLAYBOOK = 'playbook.yml'
        INVENTORY_FILE = 'inventory.yml'
        CONFIG_FILE = 'config.yml'
        ROUTER_IP = '192.168.94.12'
    }
    triggers {
        // Poll the Git repository for changes every minute
        pollSCM('* * * * *')
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository containing the Ansible playbook, inventory, and config files
                git 'https://your-git-repo-url.git'
            }
        }
        stage('Run Ansible Playbook') {
            steps {
                // Run the Ansible playbook to apply the configurations from the config file
                sh """
                    ansible-playbook ${ANSIBLE_PLAYBOOK} \
                    -i ${INVENTORY_FILE} \
                    -e config_file=${CONFIG_FILE}
                """
            }
        }
    }
    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
