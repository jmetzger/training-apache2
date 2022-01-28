# Digitalocean cloudinit 

## Example Rocky/RHEL with Apache 

  * Attention: better change password, currrently password
  * Tested on Rocky 8

```
#cloud-config
users:
  - name: 11trainingdo
    shell: /bin/bash

runcmd:
  - sed -i "s/PasswordAuthentication no/PasswordAuthentication yes/g" /etc/ssh/sshd_config
  - echo " " >> /etc/ssh/sshd_config 
  - echo "AllowUsers 11trainingdo" >> /etc/ssh/sshd_config 
  - echo "AllowUsers root" >> /etc/ssh/sshd_config 
  - systemctl reload sshd 
  - sed -i '/11trainingdo/c 11trainingdo:$6$res/PlXwgMx0Lunp$oRK58bWSJcy4ERNh.mZFTx3TfcYGWntPYPcihvUjIRQdhBv3E.OiHnEZn31ClDqtpVz7alPSY8NmTcbT8Swpn1:17476:0:99999:7:::' /etc/shadow
  - echo "11trainingdo ALL=(ALL) ALL" > /etc/sudoers.d/11trainingdo
  - chmod 0440 /etc/sudoers.d/11trainingdo
  - dnf install -y httpd
  - systemctl start httpd
  - systemctl enable httpd 
```
