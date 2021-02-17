Ubuntu - cloud-init image for XenOrchestra

1. Install Ubuntu on single ext4 partition
2. Install XenTools
    ```bash
    mount /dev/cdrom /mnt && bash /mnt/Linux/install.sh -n && reboot now
    ```
    Unmount Xen Tools
3. Remove conflicting Cloud-init configuration
    ```bash
    rm /etc/cloud/cloud.cfg.d/99-installer.cfg
    cd /var/lib/cloud
    rm -r instance
    ```
4. Configure Cloud-Init to use ```NoCloud```
    ```bash
    dpkg-reconfigure cloud-init
    ```
5. Update, remove root password and reboot
    ```bash
    apt-get update && apt-get upgrade -y && passwd -l root && sudo shutdown -h now
    ```
6. Convert VM to template


Centos 8 Stream - cloud-init image for XenOrchestra

1. Install Centos 8 Stream on single ext4 partition
2. Install XenTools
    ```bash
    mount /dev/cdrom /mnt && rpm -i /mnt/Linux/xe-guest-utilities-7*.x86_64.rpm -n && reboot now
    ```
    Unmount Xen Tools
3. Install Cloud-Init
    ```bash
    yum install cloud-init cloud-utils-growpart
    ```
4. Configure Cloud-Init to use ```NoCloud```
    ```bash
    vi /run/cloud-init/cloud.cfg
        ```
5. Update, remove root password and reboot
    ```bash
    yum update -y && passwd -l root && sudo shutdown -h now
    ```
6. Convert VM to template