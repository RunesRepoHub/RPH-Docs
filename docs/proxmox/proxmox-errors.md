
# Proxmox Errors
These are the error that I have found within Proxmox.

![pic](../img/proxmox-errors.jpg)

## VM Errors 

??? failure "Windows ISO Fail to boot"
    
    ### Windows ISO Fail to boot
    This error seems to have something to do with, not having QEMU Guest Agent installed/enabled from the Proxmox VM wizard.

??? success "*Resolved by*"

    Install/enable QEMU Guest Agent in Proxmox VM wizard before booting the VM for the first time

----------------------------

??? failure "Windows 10 Template Blue Screen"
    
    ### Windows 10 Template Blue Screen
    This error has been “created” by making a VM, that runs an completely fresh installation of windows 10, without any updates or software installed. 
    
    Then powering the VM down and making it to a Proxmox template. When it has been made into a template then remove the CD/DVD drive. 

??? success "*Resolved by*"

    If you don’t care about the CD/DVD drive, just leave it be. The missing drive is what is causing Windows to blue screen. If you have already remove the drive, just re-added it again but make sure it is the right ISO you pick.

----------------------------

??? failure "Proxmox Virtual Environment 7.2-11 Live Migration"
    
    ### Proxmox Virtual Environment 7.2-11 Live Migration
    This problem have been covered by Proxmox's own forum.

    Xeon(R) Bronze 3106 <<--->> Xeon(R) CPU E5-2650 v2 kernel 5.15

    ----------------------------
    When migrating Xeon(R) CPU E5-2650 v2 -->> Xeon(R) Bronze 3106 

    --> *Everything is ok, VM is working*

    ----------------------------
    When migrating Xeon(R) Bronze 3106 -->> Xeon(R) CPU E5-2650 v2 

    --> *VM freezes, requires full VM shutdown and power on*

??? success "*Resolved by*"
    
    Installing pve-kernel-5.19 repository
    ```
    apt install pve-kernel-5.19
    ```

    After restarting both PVE servers they are running on pve-kernel-5.19.7-1-pve and now

    -----------------------------
    When migrating Xeon(R) CPU E5-2650 v2 -->> Xeon(R) Bronze 3106 

    --> *Everything is ok, VM works and does not freeze*

    -----------------------------
    When migrating Xeon(R) Bronze 3106 -->> Xeon(R) CPU E5-2650 v2 

    --> *Everything is ok, VM is running and not freezing*

    -------------

--------------------

## VM Internet Access


??? failure "Tailscale VPN On a Proxmox LXC Container"
    
    ### Tailscale VPN On Proxmox LXC Container
    This issue has been found when trying to use tailscale on a Proxmox LXC Container. 

    Tailscale can be installed without any problems, but when you try to run the `Sudo tailscale up` command it will return and error saying something along the lines of tailscale is not running try to.... and no matter what you try on the VM it will not be able to start tailscale.

??? success "*Resolved by*"
    
    This solution will fix any VPN you want to run such as Tailscale and OpenVPN
    ```
    cd /etc/pve/lxc
    ```

    Find the vmid of the LXC Container and then copy the lines below into the LXC Containers config.
    (Just put it below the lines already there)

    ```
    lxc.cgroup.devices.allow: c 10:200 rwm 
    lxc.mount.entry: /dev/net/tun dev/net/tun none bind,create=file
    ```

    **AND DON'T FORGET TO REBOOT THE LXC CONTAINER AFTER...**

---------------------------

## Proxmox Node NIC Error

??? failure "NIC Error"
    I just went through this issue and thought I should share. This seems more like a motherboard issue than a proxmox/networking one but I'm pretty inexperienced w/ linux.

    TL/DR: adding second nvme drive to server caused the network interface names to change by +1 each making the webui unreachable - fix by changing the names in /etc/network/interfaces and restarting the network service.

    Bug:
    I have 2 nvme drives that were purchased at different times. One already in operation w/ the system and the other to be installed. When the second nvme drive was installed the webui would be unreachable. Did not matter in which order the nvme drives were placed, it would still mess up.



??? success "*Resolved by*"
    Fix:
    Viewed my network interfaces:
    ```
    $ nano /etc/network/interfaces
    ```

    took note that the two interface names were enp39s0 and enp45s0 and the vmbro0 was pointing to enp45s0
    then ran these two commands to view interface status:
    ```
    $ ip -br -c link show
    $ ip -br -c addr show
    ```

    When these were ran, it showed the interface names as enp40s0 and enp46s0.
    I then went back to /etc/network/interfaces and modified the file w/ the new info; so enp39s0 and enp45s0 and the vmbro0 pointing to enp45s0 --> enp40s0 and enp46s0 and the vmbro0 pointing to enp46s0 now

    I then flushed the ip info on all interfaces and then restarted the networking service:
    ```
    $ ip addr flush enp40s0
    $ ip addr flush enp46s0
    $ ip addr flush vmbr0
    $ systemctl restart networking
    ```
    
    This let me to be able to reach the webui once again.

    This happened on my asrock x570 creator, I'm assuming some funky chipset stuff is going on as I'm fairly certain the first nvme slot goes to the cpu and the second goes to chipset.