# PROJECT-7
Devops Tooling Website Solution
1. Spin up a new EC2 instance with RHEL Linux 8 Operating System.
![image](https://user-images.githubusercontent.com/113097621/214419212-15bc8309-7288-4ff8-8f1c-19282114dba4.png)

Creating VOlumes
![image](https://user-images.githubusercontent.com/113097621/214422503-51e3265a-5d7b-495a-911b-7e6dffbcca04.png)

INstalling LVM package
sudo yun install lvm2 -y
![image](https://user-images.githubusercontent.com/113097621/214424883-907593da-a3b2-4b99-aeb0-cbe0b5f6803e.png)

sudo lvmdiskscan
![image](https://user-images.githubusercontent.com/113097621/214425400-0a96039d-2f53-42c4-a7be-c5f2d02f63be.png)

Create Physical Volume
![image](https://user-images.githubusercontent.com/113097621/214426424-9ebeaf11-3156-4f05-a26d-981eb83577a5.png)

sudo pvs to CHeck for physical Volume
![image](https://user-images.githubusercontent.com/113097621/214427878-04d834c0-5b68-473d-b4d1-942295a6291b.png)


![image](https://user-images.githubusercontent.com/113097621/214429217-430f0459-d74c-4874-9da6-12bcad1f09a3.png)

Create Logical Volumes
![image](https://user-images.githubusercontent.com/113097621/214431251-05ab5837-c785-4766-8ca7-67c60cc40dc4.png)

 Format disks as ext4 you will have to format them as xfs
 ![image](https://user-images.githubusercontent.com/113097621/214433127-291421bc-7bc7-40ae-8c4a-8aa22f51f5c5.png)

![image](https://user-images.githubusercontent.com/113097621/214433288-2c842d56-05a3-4e6d-9f3f-849152fadc6f.png)

![image](https://user-images.githubusercontent.com/113097621/214433393-d33ec360-63ca-4eb4-9aa6-dad5634ffe5c.png)

Create mount points 
![image](https://user-images.githubusercontent.com/113097621/214433920-2cd560b3-11ab-4eff-b601-ebad97295cec.png)
![image](https://user-images.githubusercontent.com/113097621/214434344-c7bb6871-0daf-4ef0-b849-203ebc852169.png)

Install NFS server
sudo yum -y update
sudo yum install nfs-utils -y
sudo systemctl start nfs-server.service
sudo systemctl enable nfs-server.service
sudo systemctl status nfs-server.service
![image](https://user-images.githubusercontent.com/113097621/214434907-0716947b-ebe0-4c29-ad14-93e76ec7bcbd.png)

Make sure we set up permission that will allow our Web servers to read, write and execute files on NFS:
sudo chown -R nobody: /mnt/apps
sudo chown -R nobody: /mnt/logs
sudo chown -R nobody: /mnt/opt

sudo chmod -R 777 /mnt/apps
sudo chmod -R 777 /mnt/logs
sudo chmod -R 777 /mnt/opt

sudo systemctl restart nfs-server.service
![image](https://user-images.githubusercontent.com/113097621/214442968-a16226e1-cba8-4068-a5bb-6ad17f208bbc.png)

Configure access to NFS for clients within the same subnet
![image](https://user-images.githubusercontent.com/113097621/214443132-fcfc5ed5-eaeb-4370-8221-e3f9a6e1a4a7.png)

sudo vi /etc/exports
![image](https://user-images.githubusercontent.com/113097621/214443289-fe809157-d6bb-4d2c-9d56-306a3f234682.png)

Check which port is used by NFS and open it using Security Groups (add new Inbound Rule)
![image](https://user-images.githubusercontent.com/113097621/214443480-2166fd23-c1c2-4f01-94e5-a84da0cdd5c0.png)

 In order for NFS server to be accessible from your client, you must also open following ports: TCP 111, UDP 111, UDP 2049
![image](https://user-images.githubusercontent.com/113097621/214444414-1cfd6414-94a8-4c31-b607-c60062ec6189.png)

Step 2 — Configure the database server
1. Install MySQL server
![image](https://user-images.githubusercontent.com/113097621/214448771-162f09e8-cae4-4ac6-a2ce-5c03bb0499a0.png)
2. Create a database and name it tooling
![image](https://user-images.githubusercontent.com/113097621/214449104-b768ae8b-b1ba-4318-8b81-8d95ff84c646.png)
3. Create a database user and name it webaccess
![image](https://user-images.githubusercontent.com/113097621/214450400-b9254ae5-c4ee-4833-9444-ca8830652740.png)
4. Grant permission to webaccess user on tooling database to do anything only from the webservers subnet cidr
![image](https://user-images.githubusercontent.com/113097621/214450543-1a0072f9-8d99-4928-b716-979f7a249aaa.png)


Step 3 — Prepare the Web Servers
Launch a new EC2 instance with RHEL 8 Operating System
Install NFS client

sudo yum install nfs-utils nfs4-acl-tools -y
![image](https://user-images.githubusercontent.com/113097621/214450699-8953f91b-b7a2-4f79-bb02-cedb36398df5.png)


Mount /var/www/ and target the NFS server’s export for apps
sudo mkdir /var/www
sudo mount -t nfs -o rw,nosuid <NFS-Server-Private-IP-Address>:/mnt/apps /var/www
![image](https://user-images.githubusercontent.com/113097621/214451028-c051a52c-b8b5-4ebf-9445-dca8f9f68753.png)
 
 Verify that NFS was mounted successfully by running df -h. Make sure that the changes will persist on Web Server after reboot:
 ![image](https://user-images.githubusercontent.com/113097621/214982273-c92cf69c-ebf3-4e1f-8b8e-3ef7bbcb60aa.png)

Install Remi’s repository, Apache and PHP
sudo yum install httpd -y
![image](https://user-images.githubusercontent.com/113097621/214984406-1c311f3a-e91e-413a-bc35-88f5dbe24dea.png)

sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
![image](https://user-images.githubusercontent.com/113097621/214984982-1c76d25c-1899-4c40-bc30-85a0cdda8a0d.png)

sudo dnf install dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm
![image](https://user-images.githubusercontent.com/113097621/214984579-b93fcc24-1bb0-4718-a135-7eb054928420.png)

sudo dnf module reset php
![image](https://user-images.githubusercontent.com/113097621/214985376-ecb2322d-b661-48b6-a751-615001b06fa4.png)

![image](https://user-images.githubusercontent.com/113097621/214985656-52a383b1-df46-40a2-a8a9-cac2763848ff.png)
 
STEPS 1 TO 5 WAS REPEATED FOR THE 3 WEB SERVERS
 
 
Verify that Apache files and directories are available on the Web Server in /var/www and also on the NFS server in /mnt/apps
![image](https://user-images.githubusercontent.com/113097621/214992205-3b161c1b-a19d-49b3-8a5d-13d535d9c0ab.png)
![image](https://user-images.githubusercontent.com/113097621/214992258-c6056b08-f5bc-4dd8-ab3c-4147cf7bf574.png)
 
 ![image](https://user-images.githubusercontent.com/113097621/214992409-394c3ba2-fe69-4537-95d5-4d57e250a7da.png)
 
 Locate the log folder for Apache on the Web Server and mount it to NFS server’s export for logs. Repeat step №4 to make sure the mount point will persist after reboot.
 ![image](https://user-images.githubusercontent.com/113097621/214993443-1b499d1f-a0d3-4a03-ab49-cbea60185194.png)

 
 Open the website in your browser 
 ![image](https://user-images.githubusercontent.com/113097621/214998058-fa8f3c1d-f4f8-4a52-b02e-36a02d436e44.png)










