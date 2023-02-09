# Setup/Install Ansible

![ansible](../img/ansible-ubuntu.png)

??? info "Introduction"

    *This is how I automated the deployment of a test environment, with 2 Windows Servers VMs as DC controllers and 3 Windows 10 VMs as client. All 3 clients have been sign into the Windows AD, and so have both the Windows Servers.*

??? warning "This Was Made for..."

    *This was made for and deployed onto a Proxmox Server with ansible running on a Ubuntu VM from my Windows laptop as controller.*

## Installation on Ubuntu VM

--------------------

??? example "Install sudo"

    ### Install sudo
    This will be needed later for sudo nano.
    ```
    apt-get install sudo 
    ```


??? example "Install curl"

    ### Install curl
    This will be needed later to easier download the playbooks from github and install TailScale VPN
    ```
    sudo apt install curl
    ```
    Or
    ```
    sudo apt-get install curl
    ```



??? example "Install pip"

    ### Install pip
    This will be needed later to download/install ansible and it's modules and also update blowfish.
    ```
    sudo apt-get install python3 python3-pip -y
    ```



??? example "Install Ansible"

    ### Install Ansible
    Install Ansible and make sure the everything is as it should.
    ```
    sudo pip3 install ansible 
    ```
    Check that Ansible was installed with the command below.
    ```
    ansible --version
    ```

----------------

## Prep Proxmox Server

??? example "Install Proxmoxer"

    ### Install Proxmoxer
    This will be needed to deploy VMs via Ansible on the Proxmox server.
    This has to be done on the Proxmox server ifself.
    ```
    pip install proxmoxer
    ```
    ```
    pip install requests
    ```
    ```
    pip install paramiko
    ```
    ```
    pip install openssh_wrapper
    ```



??? example "Update Blowfish"

    ### Update Blowfish
    Removes a warning when using ssh of Blowfish being deprecated. 
    (Do this to both Proxmox Server and Ubuntu VM)
    ```
    pip install blowfish
    ```


--------------------

## Configuration of Ansible controller

![ansible-ssh](../img/Ansible-ssh.png)

??? example "Make Ansible.cfg"
    
    If you can't see any config file set for Ansible when you enter:
    ```
    Ansible --version
    ```

    All you have to do is make a folder in `/etc`

    You can do this with this command
    ```
    cd /etc

    sudo mkdir ansible
    ```

    When you have made a ansible folder we can `cd` into it
    ```
    cd /etc/ansible
    ```

    In this folder we need to make a file named ansible.cfg
    ```
    sudo nano ansible.cfg
    ```

    When you get into the nano editer all you have to do is copy and paste the code from the link below or use this command.

    ```
    cd /etc/ansible
    sudo wget https://gist.githubusercontent.com/alivx/2a4ca3e577ead4bd38d247c258e6513b/raw/fe2b9b1c7abc2b52cc6998525718c9a40c7e02a5/ansible.cfg
    ```

    [Github (Ansible.cfg)](https://gist.github.com/alivx/2a4ca3e577ead4bd38d247c258e6513b){ .md-button}


??? example "Modify Hosts"

    ### Modify Hosts
    After installing Ansible, the file /etc/hosts file is created automatically. 
    In this file, we are required to add our managed nodes.

    In the file, add your managed nodes as below.

    ```
    [Node1]
    192.168.100.118
    [Node2]
    192.168.100.119
    ```



??? example "Modify Ansible.cfg"

    ### Modify Ansible.cfg 
    Find and change the following settings in 
    ```
    sudo nano /etc/ansible/ansible.cfg
    ```
    ```
    inventory = /etc/ansible/hosts

    forks = 5
    sudo_user = root

    remote_user = root

    become=True
    become_method=sudo
    become_user=root
    become_ask_pass=False
    ```



??? example "Allow root login"

    ### Allow root login
    (login to all nodes and do the following)

    To enable SSH login for a root user on Debian Linux system you need to first configure SSH server. 
    ```
    sudo nano /etc/ssh/sshd_config
    ```

    Change the following line:
    ```
    FROM:
    PermitRootLogin without-password
    
    TO:
    PermitRootLogin yes
    ```

    Once you made the above change restart your SSH server:
    ```
    # /etc/init.d/ssh restart
    [ ok ] Restarting ssh (via systemctl): ssh.service.
    ```



??? example "Push SSH key to nodes"

    ### Push SSH key to nodes
    This is done so that Ansible can use the SSH key to sign in as a user
    ```
    ssh-copy-id -i ~/.ssh/id_rsa.pub your_username@192.168.100.118
    ```



??? info "References"

    ## References 

    1. [Install and use ansible on debian linux](https://computingforgeeks.com/install-and-use-ansible-on-debian-linux/)
    2. [Blowfish](https://pypi.org/project/blowfish/)
    3. [Proxmoxer](https://pypi.org/project/proxmoxer/)
    4. [Install pip on debian](https://linuxhint.com/install-pip-on-debian-11/)
    5. [Install curl on debian](https://www.cyberciti.biz/faq/howto-install-curl-command-on-debian-linux-using-apt-get/)
    6. [Enable sudo user account debian](https://milq.github.io/enable-sudo-user-account-debian/)
