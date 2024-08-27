Keep your jenkins machine as ansible server machine keep jenkins node as ansible node

**Steps to Establish SSH Connection Between Server and Node:**

**A. On the Server (Control Machine):**

1. **Generate an SSH Key Pair:**
    - Command: `ssh-keygen -t rsa -b 4096 -C "abc@example.com"`
    - **Purpose:** Creates a public/private key pair that can be used for secure, passwordless SSH connections.
2. **Copy the SSH Public Key to the Node:**
    - Command: `ssh-copy-id ansiblenode@<Node-IP>`
    - **Purpose:** Copies the server's public key to the node's `~/.ssh/authorized_keys` file, allowing passwordless SSH login from the server to the node.

**B. On the Node (Target Machine):**

1. **Create the `ansible` User (If Not Already Created):**
    - Command: `sudo adduser ansiblenode`
    - **Purpose:** Creates a user that will be used for SSH connections from the server.
2. **Set Up SSH Directory and Permissions:**
    - Commands:
        - `mkdir -p ~/.ssh`
        - `chmod 700 ~/.ssh`
    - **Purpose:** Ensures the `~/.ssh` directory exists and has the correct permissions for secure storage of the public key.
3. **Manually Add the Public Key (If Needed):**
    - Command: `nano ~/.ssh/authorized_keys`
    - **Purpose:** Stores the server's public key in the node’s `authorized_keys` file, enabling passwordless SSH access.
4. **Check and Configure SSH Settings:**
    - Command: `sudo nano /etc/ssh/sshd_config`
    - **Purpose:** Ensures SSH is configured to accept public key authentication by checking or setting `PubkeyAuthentication yes` and `AuthorizedKeysFile .ssh/authorized_keys`.
5. **Restart the SSH Service:**
    - Command: `sudo systemctl restart sshd`
    - **Purpose:** Applies the SSH configuration changes.

**C. Testing and Verification:**

1. **Test SSH Connection from Server to Node:**
    - Command: `ssh ansible@<Node-IP>`
    - **Purpose:** Confirms that the server can connect to the node without a password, verifying that the SSH key setup is correct.
- Once the connection is done then we execute the playbook,
- this playbook ask pass when we execute it for that we use command as

  `ansible-playbook -i /etc/ansible/hosts/ playbook_name.yml —ask-become-pass` 

-**Ansible Assignment 1: (CI/CD)**
-**A. CI/CD Integration**:
     -*1. Agent Node Configuration*:
            - On the agent node, create a user specifically for the Jenkins agent.
            - Configure the Jenkins agent with SSH credentials, using the following details:
            - Username: username (the user created on the agent node i.e. `ansiblenode`)
            - Private Key: The SSH private key from the remote server. `cat ~/.ssh/id_rsa`
            - Playbook Configuration: In your Ansible playbook, specify the host as ansible_node (which corresponds to the agent node label).
- **B. Manage SSH Credentials**:
  - *1. Copy and Set Permissions*:
            - Copy the SSH private key to Jenkins's directory and adjust permissions:
            `sudo cp /home/vagrant/.ssh/id_rsa /var/lib/jenkins/.ssh/id_rsa
            sudo chown jenkins:jenkins /var/lib/jenkins/.ssh/id_rsa
            sudo chmod 600 /var/lib/jenkins/.ssh/id_rsa`
