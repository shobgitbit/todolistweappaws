
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
