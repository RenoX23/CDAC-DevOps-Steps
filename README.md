# CDAC-DevOps-Steps


🚀 DevOps Lab Ultimate Cheat Sheet

Git | Docker | Jenkins | Terraform | AWS

This repository documents the complete step-by-step procedures followed during DevOps lab assignments and examinations — from installation to implementation to execution.

Focus: Lab exams, hands-on execution, and real-world DevOps workflows.
📌 Tech Stack Covered

Git & GitHub

Docker

Jenkins

Terraform

AWS (IAM, EC2, S3)

1️⃣ Git – Version Control
🔹 Install Git (Ubuntu)
```
sudo apt update
sudo apt install git -y
git --version
```
🔹 Configure Git (Mandatory)
```
git config --global user.name "Your Name"
git config --global user.email "yourmail@gmail.com"
git config --list
```
🔹 Initialize Local Repository
```
mkdir devops-lab
cd devops-lab
git init
```

create a file:
```
nano README.md
```
🔹 Git Workflow (Core Lab Flow)
```
git status
git add .
git commit -m "Initial commit"
```
🔹 Push to GitHub
```
git branch -M main
git remote add origin https://github.com/<username>/<repo>.git
git push -u origin main
```
⚠️ Common Git Errors
| Error                                 | Reason          |
| ------------------------------------- | --------------- |
| `src refspec main does not match any` | No commit done  |
| `not a git repository`                | Wrong directory |

2️⃣ Docker – Containerization
🔹 Install Docker
```
sudo apt update
sudo apt install docker.io -y
docker --version
```
🔹 Start & Enable Docker
```
sudo systemctl start docker
sudo systemctl enable docker
```
🔹 Docker Basic Commands
```
docker images
docker ps
docker ps -a
```
🔹 Dockerfile (Exam-Standard)
```
FROM ubuntu:20.04
RUN apt update && apt install -y nginx
CMD ["nginx", "-g", "daemon off;"]
```

🔹 Build Docker Image
```
docker build -t nginx-app .
```

🔹 Run Docker Container
```
docker run -d -p 8080:80 nginx-app
```

🔹 Verify
```
docker ps
curl localhost:8080
```

🔹 Push Image to DockerHub (Optional)
```
docker login
docker tag nginx-app <username>/nginx-app
docker push <username>/nginx-app
```

3️⃣ Jenkins – CI/CD Automation
🔹 Install Java (Mandatory)
````
sudo apt install openjdk-11-jdk -y
java -version
````

🔹 Install Jenkins
```
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
```

🔹 Start Jenkins
```
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins
```

🔹 Access Jenkins
```
http://localhost:8080
```

Get initial password:
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

🔹 Jenkins Freestyle Job (Lab Standard)

New Item → Freestyle Project

Source Code Management → Git

Enter GitHub Repo URL

Build Step → Execute Shell
```
echo "Build Successful"
```

Save → Build Now

✅ Green build = success

🔹 Jenkins + Docker (If Required)
```
docker build -t app .
docker run -d -p 8081:80 app
```

4️⃣ Terraform – Infrastructure as Code
🔹 Install Terraform
```
wget https://releases.hashicorp.com/terraform/1.5.7/terraform_1.5.7_linux_amd64.zip
unzip terraform_1.5.7_linux_amd64.zip
sudo mv terraform /usr/local/bin/
terraform -version
```

🔹 Terraform Configuration Files
```
provider.tf
provider "aws" {
  region = "ap-south-1"
}
```
```
main.tf (EC2 Instance)
resource "aws_instance" "lab" {
  ami           = "ami-0f5ee92e2d63afc18"
  instance_type = "t2.micro"
}
```


🔹 Terraform Workflow (Must Memorize)
```
terraform init
terraform validate
terraform plan
terraform apply
```

Confirm:
```
yes
```

🔹 Destroy Resources
```
terraform destroy
```

5️⃣ AWS – Cloud Operations
🔹 IAM Setup (Lab Favorite)

Create IAM User
```
Enable Programmatic Access
```
Attach Policies:
```
AmazonEC2FullAccess

AmazonS3FullAccess
```
🔹 Configure AWS CLI
```
aws configure
```

Inputs:

```
Access Key

Secret Key

Region: ap-south-1

Output: json
```

Verify:
```
aws sts get-caller-identity
```
🔹 EC2 Instance (Manual)
```
Instance Type: t2.micro

Key Pair: .pem

Security Group: Allow SSH (22)
```
🔹 Connect to EC2
```
chmod 400 key.pem
ssh -i key.pem ec2-user@<public-ip>
```
🔹 S3 Operations
```
aws s3 mb s3://my-devops-bucket
aws s3 ls
```

Upload file:

```
aws s3 cp file.txt s3://my-devops-bucket
```

🧠 Lab Exam Strategy (Read This Twice)

Follow correct order

Speak while executing

Verify output after every step

Don’t rush

Examiner Focus Areas:

Git → commit & push

Docker → build & run

Jenkins → successful build

Terraform → apply

AWS → EC2 / S3 visibility

❌ Common Lab Failures

Skipping terraform init

Jenkins not running on port 8080

Docker permission denied

Wrong AWS region

Missing security group rules
