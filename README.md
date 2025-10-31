# network-lab-Modulo-5
SOlll Modulo V

Laboratorios del modulo V Practica 1


ifconfig

ping 192.168.1.12

ping 192.168.1.11

sudo apt install rsync 

sudo systemctl enable rsync 

sudo systemctl start rsync 

sudo systemctl status rsync 

ssh-keygen -t rsa -b 4096

ssh-copy-id felnan2@192.168.1.12

ssh felnan2@192.168.1.12

pwd 

ls

cd Escritorio/

mkdir popeye

cd popeye

touch marino{1..100}.txt

rsync -avz /home/felnan2/Escritorio/popeye/ fernando@192.168.1.11:/home/fernando/Escritorio

cd Escritorio/

nano ~/sync_script.sh

#!/bin/bash 
rsync -avz /home/felnan2/Escritorio/Popeye/ fernando@192.168.1.11:/home/fernando/Escritorio

chmod +x ~/sync_script.sh

crontab -e

* * * * * /bin/bash ~/sync_script.sh

touch /home/felnan2/Escritorio/Popeye/test_sync.txt

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Laboratorios del modulo V Practica 2

sudo apt update 

sudo apt install -y pacemaker corosync crmsh

systemctl status pacemaker corosync 

sudo nano /etc/corosync/corosync.conf

Ejemplo de configuracion 

totem {
    version: 2
    cluster_name: fernandom.p
    transport: udpu
}

nodelist {
    node {
        ring0_addr: 192.168.1.11 #Nodo1
        name: fernandom.p
        nodeid: 1
     }
     node {
         ring0_addr: 192.168.1.12 #Nodo2
         name: fernandom.p
         nodeid: 2
     }
}

quorum {
    provider: corosync_votequorum
    two_node: 1
}

logging {
    to_syslog: yes
}

sudo systemctl restart corosync          
sudo systemctl enable corosync 

sudo corosync-cmapctl | grep members

sudo systemctl start pacemaker 
sudo systemctl enable pacemaker
sudo systemctl restart pacemaker 
sudo systemctl status pacemaker 

sudo crm_mon -1

sudo crm configure property stonith-enabled=false
sudo crm configure primitive vip ocf: heartbeat:IPaddr2 \
   params ip=192.168.1.200 cidr_netmask=24 \
   op monitor interval=30s 

sudo crm configure show 

sudo systemctl restart pacemaker
sudo systemctl restart corosync
sudo systemctl status pacemaker corosync 

ping 192.168.1.200 -t

sudo reboot 

sudo crm_mon -1 

