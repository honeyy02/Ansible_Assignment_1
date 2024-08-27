# Ansible_Assignment_1
Setup Environment:
Configure your Jenkins machine as the Ansible server.
Designate your Jenkins agent node as the Ansible node.

Create and Implement Playbook:
Playbook Tasks:
Transfer a Python application from the Ansible server (Jenkins) to the Ansible node.
Execute the Python application on the Ansible node.

CI/CD Integration:

Agent Node Configuration:
On the agent node, create a user specifically for the Jenkins agent.
Configure the Jenkins agent with SSH credentials, using the following details:
Username: username (the user created on the agent node)
Private Key: The SSH private key from the remote server.
Playbook Configuration:
In your Ansible playbook, specify the host as ansible_node (which corresponds to the agent node label).


Manage SSH Credentials:
Copy and Set Permissions:
Copy the SSH private key to Jenkins's directory and adjust permissions:
sudo cp /home/vagrant/.ssh/id_rsa /var/lib/jenkins/.ssh/id_rsa
sudo chown jenkins:jenkins /var/lib/jenkins/.ssh/id_rsa
sudo chmod 600 /var/lib/jenkins/.ssh/id_rsa

Execute Jenkins Pipeline:
Run the Jenkins pipeline which utilizes the Ansible playbook to perform the tasks.
