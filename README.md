


# Tested on Ubuntu 18.04

sudo bash
apt update && apt upgrade -y && apt-get install python3-tk python3-pip -y && pip3 install tzlocal pysqlite3 && reboot

sudo bash
cd /usr/local/sbin/

git clone https://github.com/shimuldn/kms

mv kms/py-kms/ /usr/local/sbin/
rm -r kms
chmod 755 py-kms/pykms_Server.py


nano /lib/systemd/system/py-kms.service

---------------- Put everything bellow this line on py-kms.service ----------------------

[Unit]
Description=Microsoft KMS emulator
After=network.target auditd.service

[Service]
Type=simple
User=root
Group=root
WorkingDirectory=/usr/local/sbin
ExecStart=/usr/bin/python3 /usr/local/sbin/py-kms/pykms_Server.py -F /var/log/pykms_logserver.log -V INFO -s
Restart=on-failure

[Install]
WantedBy=multi-user.target
Alias=py-kms.service

---------------- Put everything before this line on py-kms.service ----------------------


systemctl daemon-reload
systemctl enable py-kms.service
systemctl start py-kms.service
systemctl status py-kms.service




# For windows activation
```
slmgr /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX  # For windows 10 pro
slmgr.vbs /skms x.x.x.x ( x.x.x.x is ip address of the server)
slmgr.vbs /ato
  ```


```
If you keed kms key check here https://docs.microsoft.com/en-us/windows-server/get-started/kmsclientkeys

Thank You
