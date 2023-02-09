# Setup Repository

![proxmox](../img/proxmox.png)

??? info "Setup Repository Proxmox Cluster"
    ## Setup Repository For Proxmox Cluster With Mixed Intel CPU Gen's
    
    Start by editing the apt source list

    ```
    nano /etc/apt/sources.list
    ```
    In the file you can delete anything already there and replace it with the lines below:

    ```
    deb http://ftp.dk.debian.org/debian bullseye main contrib

    deb http://ftp.dk.debian.org/debian bullseye-updates main contrib

    # security updates
    deb http://security.debian.org bullseye-security main contrib

    deb http://ftp.debian.org/debian bullseye main contrib
    deb http://ftp.debian.org/debian bullseye-updates main contrib

    # PVE pve-no-subscription repository provided by proxmox.com,
    # NOT recommended for production use
    deb http://download.proxmox.com/debian/pve bullseye pve-no-subscription

    # security updates
    deb http://security.debian.org/debian-security bullseye-security main contrib
    ```


??? info "Setup Repository Proxmox Backup Server"
    ## Setup Repository Proxmox Backup Server
    ```
    # echo "deb http://download.proxmox.com/debian/pbs buster pbs-no-subscription" > /etc/apt/sources.list.d/pbs-community.list
    # apt update
    # apt -y full-upgrade
    ```