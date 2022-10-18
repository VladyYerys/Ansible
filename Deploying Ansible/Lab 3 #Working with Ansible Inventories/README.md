# Working with Ansible Inventories


![Screenshot_1](https://user-images.githubusercontent.com/106797604/196341860-28260eaa-bd85-4cbd-a240-eb056dee5d37.png)

Your company decided that their backup software license was frivolous and unnecessary. Because of this, the license was not renewed. As a stop-gap measure, your supervisor has created a simple script and an Ansible playbook to create an archive of select files, depending on pre-defined Ansible host groups. You will create the inventory file to complete the backup strategy.

# Introduction
Your company decided that their backup software license was frivolous and unnecessary. Because of this, the license was not renewed. As a stop-gap measure, your supervisor has created a simple script and an Ansible playbook to create an archive of select files, depending on pre-defined Ansible host groups. You will create the inventory file to complete the backup strategy.

# Solution
Log in to the server using the provided lab credentials:

ssh ansible@<PUBLIC_IP_ADDRESS>
If you are logged in as cloud_user, switch to ansible using the same password provided for cloud_user:

su - ansible

# Configure the media Host Group to Contain media1 and media2
Create the inventory file:

touch /home/ansible/inventory
Edit the inventory file:

vim /home/ansible/inventory
Paste in the following:

[media]
media1
media2
To save and exit the file, press ESC, type :wq, and press Enter.

# Define Variables for media with Their Accompanying Values
Create a group_vars directory:

mkdir group_vars
Move into the group_vars directory:

cd group_vars/
Create a media file:

touch media
Edit the media file:

vim media
Paste in the following:

media_content: /tmp/var/media/content/
media_index: /tmp/opt/media/mediaIndex
To save and exit the file, press ESC, type :wq, and press Enter.

# Configure the webservers Host Group to Contain the Hosts web1 and web2
Move into the home directory:

cd ~
Edit the inventory file:

vim inventory
Beneath media2, paste in the following:

[webservers]
web1
web2
To save and exit the file, press ESC, type :wq, and press Enter.

# Define Variables for webservers with Their Accompanying Values
Move into the group_vars directory:

cd group_vars/
Create a webservers file:

touch webservers
Edit the file:

vim webservers
Paste in the following:

httpd_webroot: /var/www/
httpd_config: /etc/httpd/
To save and exit the file, press ESC, type :wq, and press Enter.

# Define the script_files Variable for web1 and Set Its Value to /usr/local/scripts
Move into the home directory:

cd ~
Create a host_vars directory:

mkdir host_vars
Move into the host_vars directory:

cd host_vars/
Create a web1 file:

touch web1
Edit the file:

vim web1
Paste in the following:

script_files: /tmp/usr/local/scripts
To save and exit the file, press ESC, type :wq, and press Enter.

# Testing
Return to the home directory:

cd ~
Run the backup script:

/home/ansible/scripts/backup.sh
If you have correctly configured the inventory, it should not error.

# Conclusion
Congratulations — You've completed this hands-on lab!


# Important notes:
For your convenience, Ansible has been installed on the control node.
The user ansible has already been created on all servers with appropriate shared keys for access to managed servers from the control node.
The ansible user has the same password as cloud_user.
/etc/hosts entries have been made on control1 for the managed servers.

# 1.Create the inventory File in /home/ansible/
Create the inventory file in /home/ansible/inventory.

# 2.Configure the media Host Group to Contain media1 and media2
Use an editor such as Vim to configure the media host group to contain media and media2.

# 3.Define Variables for media with Their Accompanying Values
Define the following variables for media with their accompanying values:

media_content should be set to /var/media/content/.
media_index should be set to /opt/media/mediaIndex.

# 4.Configure the webservers Host Group to Contain the Hosts web1 and web2
Configure the webservers host group to contain the hosts web1 and web2.


# 5.Define Variables for webservers with Their Accompanying Values
Define the following variables for webservers with their accompanying values:

httpd_webroot should be set to /var/www/.
httpd_config should be set to /etc/httpd/.

# 6.Define the script_files Variable for web1 and Set Its Value to /usr/local/scripts
Define the variable script_files specifically for web1. The value of script_files should be set to /usr/local/scripts.

To test your inventory, run /home/ansible/scripts/backup.sh.

If you have correctly configured the inventory, it should not error.

Note: Do not edit anything in /home/ansible/scripts/.
