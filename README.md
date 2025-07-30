## Access phpMyAdmin in browser using Docker on an EC2 instance to manage a MySQL/MariaDB database

### **Step 1: Create a MariaDB RDS Instance**

**1. Login to AWS Console →** go to RDS

**2. Click** "Create Database"

**3. Choose:**

  * **Creation method:** Standard Create

  * **Engine:** MariaDB

**4. Templates:** Free-tier

**5. Settings:**

  * **DB instance identifier:** my-mariadb

  * **Master username:** admin

  * **Master password:** yourpassword

**6. DB Instance Class:** db.t3.micro or db.t2.micro (Free-tier eligible)

**7. Storage:**

  * **Storage type:** General Purpose (SSD)

  * **Allocated storage:** 20 GiB (Free-tier)

**8. Connectivity:**

  * **VPC:** Default or custom VPC

  * **Subnet group:** Default

  * **Public access:** Yes 

  * **VPC security group:** Create new or select existing

  * **Allow MySQL/Aurora (port 3306) from EC2 security group**

**9. Leave default values for other settings**

**10. Click Create Database**

### Step 2: Launch EC2 Ubuntu Instance

**1. Go to EC2 > Instances > Launch Instance**

**2. Name:** phpmyadmin-ubuntu

**3. AMI:** Ubuntu 22.04 LTS 

**4. Instance type:** t2.micro (free-tier)

**5. Key pair:** Select or create a key

**6. Network settings:**

  * Allow SSH (port 22)
    
  * Allow HTTP (port 80)

**9. Launch the instance**

## Step 3: Connect to EC2 via SSH

``` ssh -i "your-key.pem" ubuntu@<EC2-public-IP> ```

## Step 4: Install Docker on EC2

```
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
sudo su
```

## Step 5: Run phpMyAdmin Docker Container

``` docker run -d --name phpmyadmin -e PMA-HOST=<Your-RDS-endpoint> -e PMA_PORT=3306 -p 80:80 phpmyadmin ```

## Step 6: Access phpMyAdmin

``` http://<EC2-Public-IP> ```
