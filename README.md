![Alt text](screenshots/architecture-diagram.png)

# Private-EC2-to-S3-Secure-Access-using-VPC-Gateway-Endpoint

**🧠 Project Overview**

This project demonstrates a secure AWS architecture where an EC2 instance located in a private subnet accesses an S3 bucket using a VPC Gateway Endpoint, without using an Internet Gateway or NAT Gateway.

This ensures:

* Public access is allowed only to a Bastion Host
  
* Fully private and secure communication

* Cost optimization (no NAT Gateway charges)

* Follows cloud security best practices

* Built on Amazon Web Services (AWS).

🎯 Objective

* Allow a private EC2 instance to:

* Access S3

* Upload and download files
  
* Without Internet Gateway

* Without NAT Gateway

🧰 Services Used

* VPC

* Public Subnet

* Private Subnet

* Bastion Host EC2

* Private EC2

* S3 Bucket

* VPC Gateway Endpoint

* IAM Role

* Route Tables

* Security Groups

⚙️ Implementation Steps

Step 1: Create VPC

CIDR:

10.0.0.0/16

Step 2: Create Subnets

Public Subnet:

10.0.1.0/24

Private Subnet:

10.0.2.0/24

Step 3: Create Internet Gateway

Attach to VPC

Associate with:

Public subnet Route Table

Step 4: Launch Bastion Host

Configuration:

Launch in Public Subnet

Enable Public IP

Allow Security Group:

SSH (22) → My IP

Step 5: Launch Private EC2

Configuration:

* Launch in Private Subnet

* No Public IP

* Attach IAM Role:

* AmazonS3FullAccess


Security Group:

* Allow SSH only from Bastion Host Security Group

Step 6: Create S3 Bucket

Example:

divakar-secure-s3-demo

Step 7: Create VPC Gateway Endpoint

Go to:

VPC → Endpoints → Create Endpoint

Select:

Service:

com.amazonaws.region.s3

Type:

* Gateway

Attach:

* Private Route Table

Step 8: Connect to Bastion Host

From local system:

ssh -i key.pem ec2-user@Bastion-Public-IP

Step 9: Connect to Private EC2 from Bastion

From Bastion:

ssh -i key.pem ec2-user@Private-IP

Step 10: Test S3 Access

Install AWS CLI if Ubuntu:

* sudo apt update
* sudo apt install awscli -y


Test:

* aws s3 ls


Upload:

echo "Secure Access Test" > test.txt

aws s3 cp test.txt s3://your-bucket-name/

✅ Expected Result

Private EC2:

 * Accessible only via Bastion Host

 * Successfully access S3

 * Upload file

 * No direct internet access

🔒 Security Benefits

 * Private EC2 fully isolated

 * No public IP

 * Controlled SSH access

 * Secure S3 communication

💰 Cost Optimization

 * No NAT Gateway used

 * Saved: ₹3000/month approx

 * Gateway Endpoint is Free
