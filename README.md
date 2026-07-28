# ci-cd-jenkins

1. Log in to Docker Hub

```bash
docker login
```
- [x] Entered Docker Hub username and password (or personal access token).

2.Pull Jenkins Image

```bash
docker pull jenkins/jenkins:lts
```

3. Run Jenkins Container

```bash
docker run -d --name jenkins \
  -p 8081:8080 -p 50000:50000 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v jenkins_home:/var/jenkins_home \
  jenkins/jenkins:lts
```

4.Access Jenkins

Open your browser and go to:
```bash
http://localhost:8081
```
To get the initial admin password:
```bash
docker logs jenkins
```
Copied password shown and pasted into the Jenkins setup page.

5.Install Plugins and Create Admin User

Followed the on‑screen setup wizard:

- [x] Installed recommended plugins
- [x] Created your admin account
- [x] Jenkins dashboard had appear

6. Integration

- [x] Installed Docker Pipeline plugin in Jenkins.
- [x] Configured jobs to run Docker builds using the mounted socket.

7. Configure Jenkins Job
- In Jenkins UI → New Item → Pipeline.
- Select Pipeline script from SCM.
- Choose Git and paste your repo URL.
- Created webhook in git
- Enabled GitHub hook trigger for GITScm polling
- Jenkins will automatically look for Jenkinsfile in the root of the repo

8. Storing Secrets in Jenkins

- [x] stored secrets in Jenkins Credentials.
- [x] referenced them by ID in Jenkinsfile.
- [x]  Jenkins injected them securely during pipeline execution.

9. Kubernetes with Minikube

- [x] Installed Minikube

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
- [x] Started the cluster

```bash
minikube start --driver=docker
```
- This spun up a single‑node Kubernetes cluster inside Docker.

10. ArgoCD Setup on Minikube

- [x] Created namespace
 
 ```bash
kubectl create namespace argocd
```
- [x] Installed ArgoCD

```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
-[x] Exposed ArgoCD server

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
- [x] Logged in

- Retrieved initial admin password:

```bash
  kubectl get secret argocd-initial-admin-secret -n argocd \
  -o jsonpath="{.data.password}" | base64 -d
```
- Logged in at http://localhost:8081 with admin.

- [x] Connected GitHub repo
- Added repo containing Kubernetes manifests.
- Created an ArgoCD Application pointing to that repo.

- [x] Synced Application
- Clicked Sync in ArgoCD UI.
- Jenkins pods deployed into Minikube cluster.

- [x] Verified with:
```bash
kubectl get pods -n argocd
```
<img width="685" height="121" alt="image" src="https://github.com/user-attachments/assets/2640d47a-ee26-4e1b-a612-2560bbe8ea8f" />

- Used minikube to access the service
<img width="761" height="226" alt="image" src="https://github.com/user-attachments/assets/8b2c2357-66fa-41a6-896f-d6f06a5056b8" />
-
-  copied the url and pasted in browser
<img width="956" height="481" alt="image" src="https://github.com/user-attachments/assets/7afa71fa-e6a1-4ef5-830b-241fbf4d2a03" />


10. Accesing application

- [x] Verified Deployment

- Checked pods and services:

  ```bash
  kubectl get pods -n defaut
  ```
<img width="510" height="74" alt="image" src="https://github.com/user-attachments/assets/0467158c-814a-43b3-b7b2-25e3d6253bcc" />

```bash
kubectl get svc -n default
```
<img width="536" height="54" alt="image" src="https://github.com/user-attachments/assets/4bef62ad-fb93-4803-a5ba-d51506757276" />
- Made sure pods are in Running state.

- Used Minikube to expose the service:
  ```bash
  minikube service todo-app -n default
  ```
  <img width="606" height="297" alt="image" src="https://github.com/user-attachments/assets/b7ff53d3-1351-4005-b281-bbe7991c1cee" />

 - copied the url and pasted in browser to access the application
   <img width="947" height="414" alt="image" src="https://github.com/user-attachments/assets/791d3ec3-f5a3-4e56-b14a-39ee5b83877b" />









