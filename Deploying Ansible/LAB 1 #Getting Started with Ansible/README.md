Your CIO has greenlit a proof of concept for Ansible in your environment. You are to set up an Ansible control node in a test environment and verify basic functionality. You have three demo hosts, one to be the control node (control1), and two to serve as managed nodes (node1 and node2). You must complete the following steps:

Install Ansible on the control node.
Configure the ansible user on the control node for ssh shared key access to managed nodes.
Note: do not use a passphrase for the key pair.
Create a simple Ansible inventory on the control node in /home/ansible/inventory containing node1 and node2.
Configure sudo access for Ansible on node1 and node2 so that Ansible may use sudo for any command with no password prompt.
Verify each managed node can be accessed by Ansible from the control node using the ping module. Redirect the output of a successful command to /home/ansible/output.
Important Notes:

The user ansible is already present on all servers for your convenience.
The ansible user has the same password as the cloud_user.
/etc/hosts entries are present on control1 for the managed nodes.


# 1.Install Ansible on the control node.

To install Ansible on the control node, run sudo yum install ansible.

# 2.Configure the `ansible` user on the control node for ssh shared key access to managed nodes. Do not use a passphrase for the key pair.

To create a keypair for the ansible user on the control host, run the following:
sudo su - ansible
ssh-keygen (accept all defaults: press enter for each prompt)
Copy the public key to both node1 and node2.
As the ansible user on the control host:
ssh-copy-id node1 (accept the host key if prompted, authenticate as ansible user)
ssh-copy-id node2 (accept the host key if prompted, authenticate as ansible user)

# 3.Create a simple Ansible inventory on the control node in `/home/ansible/inventory` containing `node1` and `node2`.

On the control host:
sudo su - ansible (if not already ansible user)
touch /home/ansible/inventory
echo "node1" >> /home/ansible/inventory
echo "node2" >> /home/ansible/inventory

# 4.Configure sudo access for Ansible on `node1` and `node2` such that Ansible may use sudo for any command with no password prompt.

Log in to node1 as cloud_user and edit the sudoers file to contain appropriate access for the ansible user:
ssh cloud_user@node1
sudo visudo
Add the following line to the file and save:
ansible    ALL=(ALL)       NOPASSWD: ALL
Repeate these steps for node2.

# 5.Verify each managed node is able to be accessed by Ansible from the control node using the `ping` module. Redirect the output of a successful command to `/home/ansible/output`.

To verify each node, run the following as the ansible user from the control host:
ansible -i /home/ansible/inventory node1 -m ping
ansible -i /home/ansible/inventory node2 -m ping
To redirect output of a successful command to /home/ansible/output:
ansible -i /home/ansible/inventory node1 -m ping > /home/ansible/output


