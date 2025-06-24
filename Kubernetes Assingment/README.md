## 🎯 Objective (Class Assingment)

Learn how to deploy your very first application on Kubernetes!  
We’ll use a simple NGINX web server as an example and walk through every step — from creating the file, to running commands, to checking if it worked.

---

## 🗺️ Diagram: How It Works

![ChatGPT Image Jun 23, 2025, 09_43_37 AM](https://github.com/user-attachments/assets/a418a569-9d42-40a7-a7fc-78c3e3f321c4)



---

## 📝 Step-by-Step Guide

### 1. Make the Pod Definition File (`pod.yaml`)

Everything in Kubernetes uses a YAML file. Here’s one that tells Kubernetes to run an NGINX server for us.

Copy this into a new file named `pod.yaml`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx-container
    image: nginx:1.14.2
    ports:
    - containerPort: 80
````

---

### 2. Deploy the Pod

Now we tell Kubernetes to create this pod using the command line.

Open your terminal and run:

```bash
kubectl apply -f pod.yaml
```

If it works, you should see something like this:

```
pod/nginx-pod created
```

---

### 3. Check If the Pod is Running

Let’s make sure our pod is up and running:

```bash
kubectl get pods
```

For more details (like which node it's on):

```bash
kubectl get pods -o wide
```

---

### 4. See the Logs

Let’s check the logs to make sure the NGINX server is starting correctly:

```bash
kubectl logs nginx-pod
```

---

### 5. Get More Info (For Troubleshooting)

If something doesn’t work, this command gives you a lot of helpful info:

```bash
kubectl describe pod nginx-pod
```

---

## 📷 Add Your Screenshot

![Screenshot 2025-06-17 151939](https://github.com/user-attachments/assets/4fcc397f-0c0e-4a79-8d7a-85c35fe2b588)

![Screenshot 2025-06-17 151923](https://github.com/user-attachments/assets/e9359d96-3b04-4681-afc0-22d6a066b26d)

![Screenshot 2025-06-17 151826](https://github.com/user-attachments/assets/c60aa62b-f1a4-4955-8f9c-0fd4f65bd966)

![Screenshot 2025-06-17 151815](https://github.com/user-attachments/assets/2bbdbc40-891a-4bd5-b2cf-12c0d15380d0)

![Screenshot 2025-06-17 151759](https://github.com/user-attachments/assets/9b04a89d-f4b8-4865-9fed-9957bf105343)

![Screenshot 2025-06-17 151740](https://github.com/user-attachments/assets/b6d1a632-8bfc-487c-b0a8-d86cb49a8b66)

![Screenshot 2025-06-17 151634](https://github.com/user-attachments/assets/8697e472-c2d5-44cb-a5d2-6a338bc61e2f)

![Screenshot 2025-06-17 151604](https://github.com/user-attachments/assets/2aa394d7-0e6c-4157-8b41-f01c87ca0ce1)




---

## ✔️ What Did You Just Do?

* You wrote your first Kubernetes manifest file (`pod.yaml`).
* You deployed an NGINX web server on Kubernetes.
* You checked its status and logs.
* You learned some basic troubleshooting!

---

# MongoDB + Mongo-Express on Kubernetes(TAKE HOME ASSINGMENT)

---

## 🎯 Objective

Deploy a secure, real-world, multi-tier application on Kubernetes using best practices for secrets and configuration.
This project sets up a MongoDB database and a Mongo-Express web interface, all managed by Kubernetes.

---

## 🗺️ Architecture & Workflow


![ChatGPT Image Jun 23, 2025, 10_10_29 AM](https://github.com/user-attachments/assets/785ac2e0-5679-4ae9-b572-de63fd680d71)


**Workflow:**
User → (LoadBalancer Service) → Mongo-Express Pod → (Internal Service) → MongoDB Pod (with Secrets/ConfigMaps for credentials and configs)

---

## 📝 Deployment Steps

### 1. **Create and Apply Kubernetes Secret**

* Encode your database username and password in base64 and create a Kubernetes Secret manifest for them.
* Apply the secret to your cluster.
![Screenshot 2025-06-22 010958](https://github.com/user-attachments/assets/f9985d1d-93e8-4ad7-85ba-f4d49adf2086)

### 2. **Deploy MongoDB with Internal Service**

* Write a Deployment for MongoDB and a Service to give it a stable internal address.
* Reference the secret for MongoDB credentials in the deployment.

### 3. **Create a ConfigMap for App Config**

* Make a ConfigMap for the Mongo-Express app to know the database’s internal service name.
* Apply the ConfigMap.

### 4. **Deploy Mongo-Express with External Service**

* Write a Deployment for Mongo-Express, referencing both the ConfigMap and Secret for configuration and credentials.
* Expose Mongo-Express with a Service of type LoadBalancer (or NodePort for Minikube).
![Screenshot 2025-06-22 010945](https://github.com/user-attachments/assets/949617fc-8e20-41cf-b39a-4104945dd58b)

### 5. **Access and Test**

* Use your cluster’s service management (like `minikube service mongo-express-service`) to get the external URL.
* Login to Mongo-Express in your browser with the credentials you created and confirm that it connects to MongoDB.
![Screenshot 2025-06-21 221036](https://github.com/user-attachments/assets/0c4d0e22-8481-4c60-8222-6f8a95b3f730)

![Screenshot 2025-06-22 010728](https://github.com/user-attachments/assets/c9cc1938-f3ae-401b-b520-98bdc09cc590)


### 6. **Cleanup**

* Delete all deployments, services, secrets, and configmaps you created for this assignment.

---

## 📸 Screenshots
![Screenshot 2025-06-22 010958](https://github.com/user-attachments/assets/43ff3e7e-524e-4353-9cf0-82908c93dada)
![Screenshot 2025-06-22 010945](https://github.com/user-attachments/assets/7c834546-664c-4498-83a3-5a0f994bf5cd)
![Screenshot 2025-06-22 010932](https://github.com/user-attachments/assets/cde4f19d-84dd-480b-ade8-830c71ee2568)
![Screenshot 2025-06-21 221036](https://github.com/user-attachments/assets/94fa8fdf-df8c-4d74-b29d-b7f75c08eb9e)
![Screenshot 2025-06-22 010728](https://github.com/user-attachments/assets/9837f6d9-a9a3-4ec0-8d8e-fa7572751507)
![Screenshot 2025-06-22 011037](https://github.com/user-attachments/assets/8c29cc7b-0be1-41be-9468-d7d23c51d648)


---

## 📦 Deliverables

* All YAML files for Secrets, Deployments, Services, and ConfigMaps
* Screenshot(s) of the running Mongo-Express UI
* This completed README

---

## ⚡ Difficulties Faced

* Ensuring secrets and config references were correct and consistently named
* Making the external service accessible from the browser and troubleshooting network/port issues

![Screenshot 2025-06-21 221011](https://github.com/user-attachments/assets/3e5c770e-dd33-474f-a22e-04cafeffbedc)


---

## 📝 What I Learned

* How to separate sensitive and non-sensitive config with Secrets and ConfigMaps
* How Deployments and Services work together to create a scalable, discoverable app in Kubernetes
* Real-world workflow for multi-tier application deployments

---

**Made by:**
**Sanskar Goyal**

---


