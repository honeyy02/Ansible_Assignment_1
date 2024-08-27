pipeline {
    agent none
    
    environment {
        ANSIBLE_INVENTORY = "/etc/ansible/hosts"
        ANSIBLE_PLAYBOOK = "assignment1.yml"
        ANSIBLE_VAULT_PASSWORD_FILE = "/etc/ansible/vault_pass.txt"
        SSH_PRIVATE_KEY = credentials('jenkins')
    }

    stages {
    
        stage('Run Ansible Playbook') {
            agent { label 'master' }
            steps {
                script {
                    writeFile file: '/home/vagrant/.ssh/id_rsa', text: SSH_PRIVATE_KEY, encoding: 'Base64'
                    sh """
                        chmod 600 /home/vagrant/.ssh/id_rsa
                        ansible-playbook ${ANSIBLE_PLAYBOOK} -i ${ANSIBLE_INVENTORY} --private-key=/home/vagrant/.ssh/id_rsa --vault-password-file ${ANSIBLE_VAULT_PASSWORD_FILE}
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
