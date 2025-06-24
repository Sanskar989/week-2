## 🎯 Objective

Learn how to deploy your very first application on Kubernetes!  
We’ll use a simple NGINX web server as an example and walk through every step — from creating the file, to running commands, to checking if it worked.

---

## 🗺️ Diagram: How It Works

[You (DevOps/Beginnner)]
          |
          v
   [Write pod.yaml file]
          |
          v
 [kubectl apply -f pod.yaml]
          |
          v
 [Kubernetes API Server]
          |
          v
   [Kubernetes Node]
          |
          v
 [NGINX Pod Runs on Node]
          |
          v
   [Check Status/Logs]
          |
          v
      [Success!]


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


