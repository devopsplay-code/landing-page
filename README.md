Sure! Here's your plain text README content with catchy emojis for easy copy-pasting:

---

# 🚀 Jenkins CI/CD Pipeline for Static Website Deployment on NGINX EC2

This project demonstrates a **complete Jenkins CI/CD pipeline** to deploy a static website to a **remote NGINX server (EC2)**. The pipeline automates cloning the code, and deploying the landing page to a target web server.

---

## 🧰 Tech Stack Used

* 🖥️ Jenkins (running on EC2)
* ☁️ AWS EC2 (for Jenkins & NGINX web server)
* 🔐 SSH Credentials in Jenkins
* 🧾 GitHub (static landing page repo)
* 🌐 NGINX (to host the website)

---

## 🛠️ Steps Performed

### 1. 🚀 Launch Jenkins Server

* Launched Ubuntu EC2 instance.
* Installed Jenkins.
* Configured Jenkins and installed necessary plugins.

### 2. 🌍 Launch NGINX Web Server

* Created a new Ubuntu EC2 instance.
* Installed and started NGINX.
* Verified by accessing the public IP.

```bash
sudo apt update
sudo apt install nginx -y
```

### 3. 🔑 Setup SSH Access for Jenkins

* Copied NGINX server’s private key.
* Added it as a **Jenkins secret file credential** (ID: `jenkins-ssh-key`).

### 4. 🧪 Jenkins Pipeline Script

* Created a **Declarative Pipeline** in Jenkins UI.
* Script includes:

  * GitHub clone
  * Deploy to NGINX server via `scp`

```groovy
pipeline {
    agent any

    environment {
        REMOTE_USER = 'ubuntu'
        REMOTE_HOST = 'YOUR_NGINX_PUBLIC_IP'
        REMOTE_PATH = '/var/www/html'
        PRIVATE_KEY = credentials('jenkins-ssh-key')
    }

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/devopsplay-code/landing-page.git'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    echo "$PRIVATE_KEY" > key.pem
                    chmod 400 key.pem
                    scp -i key.pem -o StrictHostKeyChecking=no -r * $REMOTE_USER@$REMOTE_HOST:$REMOTE_PATH
                    rm -f key.pem
                '''
            }
        }
    }
}
```

---

## ✅ Final Result

* Jenkins pipeline runs successfully.
* Website deployed and served via NGINX on public IP.
* 🖼️ Landing page visible from any browser.

---

## 📸 Bonus: Terminal Logo Fun

You can even display Jenkins logo in your EC2 CLI using `jp2a`:

```bash
sudo apt install jp2a -y
jp2a --colors --width=60 jenkins-logo.png
```

---

## 💡 Key Learning Outcomes

* Jenkins to EC2 SSH-based deployment
* Jenkins credential management
* Static website delivery using pipelines
* NGINX integration in CI/CD flow

---

## 📌 Tags

\#Jenkins #AWS #DevOps #CICD #Automation #NGINX #GitHub #CloudDeployment #DevOpsEngineer #PortfolioProject

---

Let me know if you want a custom GitHub repo setup or visual workflow diagram too!
