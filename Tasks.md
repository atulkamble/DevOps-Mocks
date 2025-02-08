### **🔹 DevOps Assignment Tasks with Solutions & Scripts** 🚀  

Here are **hands-on DevOps assignments** with solutions, including **shell scripts, Terraform, Ansible, Docker, Kubernetes, and Jenkins pipelines**. Each task has a **detailed solution**.

---

## **📌 Task 1: Automate Web Server Setup using Bash Script**
### **🔹 Task:**  
Write a **Bash script** to set up an **Apache web server** on an **Ubuntu EC2 instance**.

### **✅ Solution - `setup_apache.sh`**
```bash
#!/bin/bash
# Script to install Apache web server

echo "Updating system..."
sudo apt update -y

echo "Installing Apache..."
sudo apt install apache2 -y

echo "Starting Apache service..."
sudo systemctl start apache2
sudo systemctl enable apache2

echo "Creating a sample webpage..."
echo "<h1>Welcome to DevOps Automation</h1>" | sudo tee /var/www/html/index.html

echo "Web server is up and running!"
```
### **🚀 Run the script**
```bash
chmod +x setup_apache.sh
./setup_apache.sh
```
🔹 **Checks:** Visit `http://your-server-ip` to see the webpage.

---

## **📌 Task 2: Deploy an AWS EC2 Instance using Terraform**
### **🔹 Task:**  
Write a **Terraform script** to launch an **EC2 instance** in AWS.

### **✅ Solution - `main.tf`**
```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "devops_server" {
  ami           = "ami-0abcdef1234567890"  # Replace with a valid AMI ID
  instance_type = "t2.micro"

  tags = {
    Name = "DevOps-Server"
  }
}

output "instance_ip" {
  value = aws_instance.devops_server.public_ip
}
```
### **🚀 Run the Terraform Script**
```bash
terraform init
terraform apply -auto-approve
```
🔹 **Checks:** Run `terraform output` to see the instance **Public IP**.

---

## **📌 Task 3: Deploy an Nginx Web Server using Ansible**
### **🔹 Task:**  
Write an **Ansible playbook** to deploy **Nginx** on a remote server.

### **✅ Solution - `nginx_playbook.yml`**
```yaml
- name: Deploy Nginx Web Server
  hosts: web_servers
  become: yes
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Start Nginx service
      service:
        name: nginx
        state: started
        enabled: yes

    - name: Create custom homepage
      copy:
        content: "<h1>Welcome to Nginx on Ansible!</h1>"
        dest: /var/www/html/index.html
```
### **🚀 Run the Playbook**
```bash
ansible-playbook -i inventory nginx_playbook.yml
```
🔹 **Checks:** Visit `http://your-server-ip` to verify.

---

## **📌 Task 4: Dockerize a Node.js Application**
### **🔹 Task:**  
Write a **Dockerfile** to containerize a **Node.js** application.

### **✅ Solution - `Dockerfile`**
```dockerfile
FROM node:14

WORKDIR /app
COPY package.json ./
RUN npm install
COPY . .

CMD ["node", "server.js"]
```
### **🚀 Build and Run the Container**
```bash
docker build -t my-node-app .
docker run -d -p 3000:3000 my-node-app
```
🔹 **Checks:** Visit `http://localhost:3000`.

---

## **📌 Task 5: Deploy a Kubernetes Application**
### **🔹 Task:**  
Deploy a **Kubernetes pod** running an **Nginx web server**.

### **✅ Solution - `nginx-deployment.yaml`**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80
```
### **🚀 Deploy to Kubernetes**
```bash
kubectl apply -f nginx-deployment.yaml
kubectl get pods
```
🔹 **Checks:** Run `kubectl get pods -o wide`.

---

## **📌 Task 6: Create a Jenkins CI/CD Pipeline**
### **🔹 Task:**  
Create a **Jenkinsfile** to automate **build and deployment**.

### **✅ Solution - `Jenkinsfile`**
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo "Building the application..."
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo "Running tests..."
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying application..."
                sh 'scp -i my-key.pem app.js ubuntu@server:/var/www/app'
            }
        }
    }
}
```
### **🚀 Steps in Jenkins**
1. Create a **Jenkins Pipeline Job**.  
2. Add the **GitHub Repository**.  
3. Run the **Pipeline**.  

🔹 **Checks:** View logs in Jenkins UI.

---

## **📌 Task 7: Automate AWS S3 Bucket Creation using Terraform**
### **🔹 Task:**  
Write a **Terraform script** to create an **S3 bucket**.

### **✅ Solution - `s3.tf`**
```hcl
resource "aws_s3_bucket" "my_bucket" {
  bucket = "my-devops-bucket-12345"

  tags = {
    Name        = "My DevOps S3 Bucket"
    Environment = "DevOps"
  }
}
```
### **🚀 Apply the Terraform Script**
```bash
terraform init
terraform apply -auto-approve
```
🔹 **Checks:** Run `aws s3 ls` to verify.

---

## **📌 Task 8: Monitor Logs using ELK Stack**
### **🔹 Task:**  
Set up **Filebeat** to forward logs to **Elasticsearch**.

### **✅ Solution - `filebeat.yml` (Snippet)**
```yaml
filebeat.inputs:
  - type: log
    enabled: true
    paths:
      - /var/log/*.log

output.elasticsearch:
  hosts: ["http://localhost:9200"]
```
### **🚀 Start Filebeat**
```bash
sudo systemctl start filebeat
sudo systemctl enable filebeat
```
🔹 **Checks:** Run `curl -X GET "localhost:9200/_cat/indices?v"`.

---

## **📌 Task 9: Secure AWS Credentials Using Secrets Manager**
### **🔹 Task:**  
Store and retrieve **AWS credentials** securely.

### **✅ Solution - Store Secrets**
```bash
aws secretsmanager create-secret --name DevOpsDBCreds \
--secret-string '{"username":"admin","password":"P@ssw0rd"}'
```
### **✅ Retrieve Secrets**
```bash
aws secretsmanager get-secret-value --secret-id DevOpsDBCreds
```
🔹 **Checks:** Ensure secret retrieval works.

---

## **📌 Task 10: Automate User Creation in Linux**
### **🔹 Task:**  
Write a **Bash script** to create multiple users.

### **✅ Solution - `create_users.sh`**
```bash
#!/bin/bash
for user in devops1 devops2 devops3
do
  sudo useradd -m $user
  echo "User $user created"
done
```
### **🚀 Run the Script**
```bash
chmod +x create_users.sh
./create_users.sh
```
🔹 **Checks:** Run `cat /etc/passwd | grep devops`.

---

## **💡 Final Thoughts**  
These **hands-on DevOps tasks** cover **Automation, CI/CD, Terraform, Kubernetes, Jenkins, AWS, and Monitoring**. 🚀  

Let me know if you need **more advanced scripts** or **custom assignments**! 🎯
