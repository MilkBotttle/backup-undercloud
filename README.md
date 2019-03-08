# Backup the Undercloud
## Version
Pike
# Run
1. Clean garbage file in /root and /home/stack for faster backup
2. Play
```
ansible-playbook backup-undercloud/main.yaml
```
## Version
Queens
# Run
```
openstack undercloud backup
```



---
# Restoring the Undercloud
Use backup files to restore undercloud
# Version
Pike

## Case 2: Restore undercloud on a fresh node
1. Time synchoronized
```
sudo yum install -y ntp
sudo chkconfig ntpd on
sudo service ntpd stop
sudo ntpdate pool.ntp.org
sudo service ntpd restart
```
2. Extract backup files
```
mkdir /root/undercloud-extract
cd /root/undercloud-extract
gunzip UC-backup.gz /root/undercloud-extract
```
3. Copy file to current path
4. Install MariaDB service
5. Restore DB backup
6. Clean DB password to be able to reinstall the Undercloud
7. Install glance and swift base packages, and then restore their data
8. Reinstall undercloud
9. Reconnetc the restored Undercloud to the Overcloud
Having completed the steps above, the Undercloud can be expected to
automatically restore its connection to the Overcloud. The nodes
will continue to poll Orchestration (heat) for pending tasks, using
a simple HTTP request issued every few seconds.
