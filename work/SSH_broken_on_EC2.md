---
title: Work/AWS/SSH broken on EC2
---
SSH broken on EC2
===

When SSH is broken and you can not login with default key or serial
console, it is possible to use cloud-init and SSM Session Manager:

To do so add this to userdata:

```
Content-Type: multipart/mixed; boundary="//"
MIME-Version: 1.0

--//
Content-Type: text/cloud-config; charset="us-ascii"
MIME-Version: 1.0
Content-Transfer-Encoding: 7bit
Content-Disposition: attachment; filename="cloud-config.txt"

#cloud-config
cloud_final_modules:
- [scripts-user, always]

--//
Content-Type: text/x-shellscript; charset="us-ascii"
MIME-Version: 1.0
Content-Transfer-Encoding: 7bit
Content-Disposition: attachment; filename="userdata.txt"

#!/bin/bash

mkdir /tmp/ssm
cd /tmp/ssm
wget https://s3.eu-central-1.amazonaws.com/amazon-ssm-eu-central-1/latest/debian_amd64/amazon-ssm-agent.deb
sudo dpkg -i amazon-ssm-agent.deb
sudo systemctl enable amazon-ssm-agent
--//--
```

This is required so that cloud-init also runs on every start not only on
the first boot.

