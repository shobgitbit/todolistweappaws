
# AWS EC2 Setup and To-Do List Web App Deployment

## **Project Overview**
This project outlines the step-by-step instructions for creating a GitHub repository, launching an EC2 instance on AWS, and deploying a To-Do List web app on the EC2 instance.

---

## **Prerequisites**
- **GitHub Account**  
- **AWS Account**  
- **AWS CLI Installed**  
- **SSH Key Pair** to connect to the EC2 instance  
- **Basic Knowledge of Git, AWS, and Linux Commands**  

---

## **Tasks**
1. **Create a GitHub repository**  
2. **Add a README.md file in that repository**  
3. **Create a 'develop' branch in that repository**  
4. **Launch an EC2 instance in AWS**  
5. **Connect your local machine to the EC2 instance**  
6. **Add tags to the EC2 instance**  
7. **Install Nginx web server on the EC2 instance**  
8. **Host an HTML file using Nginx**  
9. **Update README.md file with project details**  

**Bonus Task:** Spin up the EC2 using AWS CLI.  
**Ultra Bonus Task:** Make a To-Do List web app, host it on the EC2 instance, and share the public IP.  

---

## **Steps to Follow**

### **1. Create a GitHub Repository**
- Go to [GitHub](https://github.com/) and log in.  
- Click **New Repository**.  
- Name the repository (e.g., **ec2-todo-app**).  
- Add a description, set visibility (Public/Private), and click **Create Repository**.  

---

### **2. Add a README.md File**
- Clone the repository to your local machine:  
  ```bash
  git clone https://github.com/your-username/ec2-todo-app.git
  cd ec2-todo-app



#### AWS



# 🚀 How to Create an AWS EC2 Instance

This guide will walk you through the steps to create and launch an AWS EC2 instance using the AWS Management Console and AWS CLI. EC2 (Elastic Compute Cloud) provides resizable compute capacity in the cloud.

---

## 📋 **Prerequisites**
Before you start, ensure you have the following:  
1. **AWS Account** — [Sign up here](https://aws.amazon.com/) if you don't have one.  
2. **IAM User with EC2 Permissions** — Best practice is to avoid using root access.  
3. **AWS CLI Installed** — [Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html).  
4. **AWS CLI Configured** — Run `aws configure` and provide your AWS Access Key, Secret Key, Region, and Output Format.  

---

## 📌 **1. Create an EC2 Instance via AWS Management Console**

1. **Log in** to the AWS Management Console.  
2. **Navigate to EC2 Dashboard** — Select "Launch Instance."  
3. **Select an Amazon Machine Image (AMI)** — Choose an operating system (e.g., Amazon Linux, Ubuntu).  
4. **Choose an Instance Type** — Select instance size (e.g., t2.micro for Free Tier).  
5. **Configure Instance Details** — Set the network, subnet, and auto-assign IPs.  
6. **Add Storage** — Choose volume size and type (default is 8 GiB SSD).  
7. **Add Tags** — Tag your instance (optional but recommended for identification).  
8. **Configure Security Group** — Allow inbound ports (e.g., port 22 for SSH).  
9. **Launch** — Review and launch your instance. You may be prompted to create or use an existing key pair.  
10. **Access Instance** — Use SSH to connect to your instance.  

---

## 📌 **2. Create an EC2 Instance via AWS CLI**

### **Step 1: Define Variables**
```bash
export INSTANCE_NAME="MyEC2Instance"
export AMI_ID="ami-0c02fb55956c7d316" # Amazon Linux 2 AMI
export INSTANCE_TYPE="t2.micro"
export KEY_NAME="my-key-pair"
export SECURITY_GROUP="my-security-group"
export SUBNET_ID="subnet-xxxxxxx"
```

### **Step 2: Create Security Group (If Not Created)**
```bash
aws ec2 create-security-group --group-name $SECURITY_GROUP --description "My Security Group"
aws ec2 authorize-security-group-ingress   --group-name $SECURITY_GROUP   --protocol tcp --port 22 --cidr 0.0.0.0/0
```
> ⚠️ **Warning:** Allowing access from `0.0.0.0/0` exposes port 22 to the entire internet. Restrict it to your IP range for better security.

### **Step 3: Launch the Instance**
```bash
aws ec2 run-instances   --image-id $AMI_ID   --count 1   --instance-type $INSTANCE_TYPE   --key-name $KEY_NAME   --security-groups $SECURITY_GROUP   --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value='$INSTANCE_NAME'}]'
```
> 📘 **Note:** Replace `subnet-id` with the subnet you want to launch the instance in if required.  

### **Step 4: View the Instance Details**
```bash
aws ec2 describe-instances --filters "Name=tag:Name,Values=$INSTANCE_NAME"
```

---

## 📌 **3. Access Your EC2 Instance**

To access your instance, use SSH:  
```bash
ssh -i "my-key-pair.pem" ec2-user@<EC2_PUBLIC_IP>
```

> 🔐 **Note:** Ensure that `my-key-pair.pem` has correct permissions.  
```bash
chmod 400 my-key-pair.pem
```

---

## 📌 **4. Stop, Start, and Terminate an EC2 Instance**

**Stop an instance**:  
```bash
aws ec2 stop-instances --instance-ids i-xxxxxxxxxxxxxxxxx
```

**Start an instance**:  
```bash
aws ec2 start-instances --instance-ids i-xxxxxxxxxxxxxxxxx
```

**Terminate an instance**:  
```bash
aws ec2 terminate-instances --instance-ids i-xxxxxxxxxxxxxxxxx
```
> ⚠️ **Warning:** Terminating an instance deletes its data unless you have persistent storage (like EBS volumes).

---

## 📌 **Common Troubleshooting**
1. **Permission Denied on SSH?** — Ensure `chmod 400 my-key-pair.pem` was applied.  
2. **Instance Not Reachable?** — Check security group rules (port 22 must be open).  
3. **Can’t Find Key Pair?** — You cannot download it after creation. Generate a new one if lost.  

---

## 📘 **Useful Links**
- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)  
- [AWS CLI Reference](https://docs.aws.amazon.com/cli/latest/reference/)  

---

🎉 **Congratulations! You've successfully created an AWS EC2 instance!**  
