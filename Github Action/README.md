# 🚀 Full CI/CD Pipeline: Node.js App to AWS EC2 with GitHub Actions & Docker

## 📑 Overview

This project demonstrates **end-to-end DevOps automation**:  
We containerized a simple Node.js Express application, set up CI/CD using **GitHub Actions**, and deployed it directly to an **AWS EC2 instance** using Docker.  
The goal: Whenever we push to the `main` branch, the app is automatically rebuilt, containerized, and redeployed in production on our EC2 instance.

---
## Architecture

![ChatGPT Image Jun 23, 2025, 02_49_51 AM](https://github.com/user-attachments/assets/02345269-4175-4d17-844d-42be282c1412)


## 🛠️ Steps to Complete the Assignment

### 1. **Setting Up the Project**

- First, I made a new folder for my project and opened it in the terminal.
- I initialized a Node.js app and installed Express:
  ```bash
  mkdir github-actions-demo
  cd github-actions-demo
  npm init -y
  npm install express


* I wrote a simple Express app in `app.js` that just says hello and shows a version.
* I added a `Dockerfile` so the app could run in a container.

---

### 2. **Uploading My Code to GitHub**

* I started using Git by running:

  ```bash
  git init
  git add .
  git commit -m "Initial commit"
  ```
* I created a new repository on GitHub and added it as a remote:

  ```bash
  git remote add origin https://github.com/<my-username>/<my-repo>.git
  git branch -M main
  git push -u origin main
  ```

---

### 3. **Creating the CI/CD Workflow**

* I learned about GitHub Actions and made a new folder and file:
  `.github/workflows/cicd-pipeline.yml`
* I copied a workflow that had two main parts:

  * **Build and Push:** Build my Docker image and push it to GitHub’s Container Registry.
  * **Deploy:** Log into my AWS EC2 instance, pull the Docker image, and run it.
* The workflow is set to run every time I push to the `main` branch.

---

### 4. **Launching an AWS EC2 Instance**

* I logged into AWS and created a new EC2 virtual machine (Amazon Linux).
* I made sure to download the `.pem` key file so I could connect with SSH.
* In the security group settings, I opened port **22** for SSH and port **3000** for the app.
* I connected using:

  ```bash
  ssh -i path/to/key.pem ec2-user@<ec2-public-ip>
  ```
* On the EC2, I installed Docker and started it:

  ```bash
  sudo yum update -y
  sudo yum install -y docker
  sudo systemctl start docker
  sudo systemctl enable docker
  sudo usermod -aG docker ec2-user
  exit
  # Then reconnected to use Docker as my user
  ```

---

### 5. **Adding My Secrets to GitHub**

* In my repo, I went to Settings > Secrets and variables > Actions.
* I added:

  * `EC2_HOST`: The public IP address of my EC2
  * `EC2_USERNAME`: `ec2-user`
  * `EC2_SSH_KEY`: The entire PEM file (copied exactly, no changes)
* This lets GitHub Actions log in to my EC2 for automated deployment.

---

### 6. **Triggering the Pipeline and Verifying**

* I made a small change or empty commit and pushed to main:

  ```bash
  git commit --allow-empty -m "Trigger pipeline"
  git push origin main
  ```
* In the GitHub Actions tab, I watched as my workflow built the image and tried to deploy.
* If there were issues, I checked the logs and fixed them as I learned (sometimes had to re-upload the SSH key).

---

### 7. **Checking the Deployment**

* I SSH’d into my EC2 and ran:

  ```bash
  docker ps
  ```

  to check if my app container was running.
* Then, I opened a browser to `http://<ec2-public-ip>:3000` to see my app live!

---

### 8. **Debugging (Learning Experience!)**

* If deployment failed, I checked my GitHub Actions logs for errors.
* I made sure the PEM file was correct in secrets, and that ports were open.
* Sometimes, I manually pulled and ran the image on EC2 to check if it worked.

---

---

## 🖼️ Result Screenshot

![Screenshot 2025-06-23 020921](https://github.com/user-attachments/assets/b8f25c01-87a4-4af7-958d-ebb32ccff018)

![Screenshot 2025-06-23 020859](https://github.com/user-attachments/assets/49177a73-45b6-4aaf-a72c-17de46963f81)

![Screenshot 2025-06-23 020807](https://github.com/user-attachments/assets/0e4d30bc-f2f5-4021-b27a-409da56c317f)

![Screenshot 2025-06-23 020756](https://github.com/user-attachments/assets/4dc00280-bf16-4a70-8f8a-d325d926d7a8)

![Screenshot 2025-06-23 020744](https://github.com/user-attachments/assets/6ee0f3b2-1d98-4552-95a3-eae310d7b506)

![Screenshot 2025-06-23 020729](https://github.com/user-attachments/assets/24b636a4-788f-45cf-89dd-e2457cf8ba3e)

![Screenshot 2025-06-23 020714](https://github.com/user-attachments/assets/4d7ae985-0b43-469f-9dfa-9dfae09aec43)

![Screenshot 2025-06-23 020714](https://github.com/user-attachments/assets/da5755dc-caed-4a24-b94b-e75d95811293)

![Screenshot 2025-06-23 020821](https://github.com/user-attachments/assets/a10e4125-58d3-4dd6-8213-8c0f209b6413)


![Screenshot 2025-06-23 020627](https://github.com/user-attachments/assets/a9a85ef1-e1cb-4697-b021-85619a4a655e)


---

## 📦 Deliverables

- Node.js source code and `Dockerfile`
- CI/CD pipeline definition: `.github/workflows/cicd-pipeline.yml`
- Deployed, running application on AWS EC2 (`http://<your-ec2-public-ip>:3000`)
- GitHub repository with **all code, workflow, and documentation**

---

## ⚡ Difficulties Faced & How I Solved Them

### 1. **SSH Authentication Issue in GitHub Actions**
> The most time-consuming challenge was ensuring the correct PEM file was pasted as a GitHub secret (`EC2_SSH_KEY`).  
> Although SSH worked from my laptop, GitHub Actions failed until I re-copied and pasted the exact PEM file contents with no extra spaces or lines.

### 2. **Docker Image Tag Confusion**
> Initially, the pipeline failed to pull the correct image because it was pushing with the `main` tag but the deploy step was referencing an incorrect or missing tag/digest.  
> Updating the workflow to consistently use the `main` tag for both build and deploy steps solved the issue.

---

## 💡 Key Takeaways

- Real-world CI/CD needs attention to **secret management** and **consistent tagging**.
- Debugging cloud automation is about careful reading of logs and cross-verifying each configuration step.
- **Always check your SSH key and Docker tags!**

---

## 📝 Author

*Sanskar989 — DevOps Intern

