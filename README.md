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
![image](https://user-images.githubusercontent.com/113097621/214434907-0716947b-ebe0-4c29-ad14-93e76ec7bcbd.png)
