pipeline {
    agent any
    
    environment {
        ANSIBLE_INVENTORY = "/etc/ansible/hosts"
        ANSIBLE_PLAYBOOK = "/etc/ansible/playbook/assignment1.yml"
        ANSIBLE_VAULT_PASSWORD_FILE = "/etc/ansible/vault_pass.txt"
    }

    stages {
    
        stage('Run Ansible Playbook') {
            steps {
                script {
                    sh """
                      sudo  ansible-playbook ${ANSIBLE_PLAYBOOK} -i ${ANSIBLE_INVENTORY} --private-key=/home/vagrant/.ssh/id_rsa --vault-password-file ${ANSIBLE_VAULT_PASSWORD_FILE}
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Ansible Playbook executed successfully!'
        }
        failure {
            echo 'Ansible Playbook failed to execute.'
        }
    }
}
