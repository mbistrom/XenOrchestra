# Create cloud-init image for XenOrchestra

## Ubuntu 20.04.2

1. Install Ubuntu on single ext4 partition
2. Install XenTools

    ```bash
    mount /dev/cdrom /mnt && bash /mnt/Linux/install.sh -n && reboot now
    ```

3. Unmount Xen Tools

4. Remove conflicting Cloud-init configuration

    ```bash
    rm /etc/cloud/cloud.cfg.d/99-installer.cfg
    cd /var/lib/cloud
    rm -r instance
    ```

5. Configure Cloud-Init to use ```NoCloud```

    ```bash
    dpkg-reconfigure cloud-init
    ```

6. Update, remove root password and shutdown

    ```bash
    apt-get update && apt-get upgrade -y && passwd -l root && sudo shutdown -h now
    ```

7. Convert VM to template

## Centos / Rocky / Alma Linux

1. Install Centos 8 Stream on single ext4 partition
2. Install XenTools

    ```bash
    mount /dev/cdrom /mnt && rpm -i /mnt/Linux/xe-guest-utilities-7*.x86_64.rpm && reboot now
    ```

3. Unmount Xen Tools

4. Install Cloud-Init

    ```bash
    yum install cloud-init cloud-utils-growpart
    ```

5. Configure Cloud-Init to use ```NoCloud```

    ```bash
    vi /run/cloud-init/cloud.cfg
    ```

6. Update, remove root password and shutdown

    ```bash
    yum update -y && passwd -l root && sudo shutdown -h now
    ```

7. Convert VM to template
