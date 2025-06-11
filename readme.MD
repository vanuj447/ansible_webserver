# Apache Deployment using Ansible and Jenkins with Slack Notifications

This project automates the deployment of an Apache web server on a remote Ubuntu machine using **Ansible**. The process is triggered by a **Jenkins pipeline**, which also sends **Slack notifications** for build status updates.

## 🔧 Tools Used
- Jenkins (CI/CD pipeline)
- Ansible (configuration management)
- Apache2 (web server)
- Slack (build notifications)
- Git (source code)

## ⚙️ How It Works
1. Jenkins triggers the pipeline on code push.
2. Ansible installs Apache and deploys website files on the remote server.
3. Slack sends notifications for approval, success, or failure.

## 📁 Files
- `apache-install.yml` – Ansible playbook to install and configure Apache
- `inventory.ini` – Target server info
- `Jenkinsfile` – Defines pipeline steps and Slack integration

## ✉️ Author
**Anuj Verma**  
[GitHub](https://github.com/vanuj447) | [LinkedIn](https://linkedin.com/in/anuj-verma-998b231b7)

