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

-[x] Created namespace
 
 ```bash
kubectl create namespace argocd
```
-[x] Installed ArgoCD

```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
-[x] Exposed ArgoCD server

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
-[x] Logged in

- Retrieved initial admin password:

```bash
  kubectl get secret argocd-initial-admin-secret -n argocd \
  -o jsonpath="{.data.password}" | base64 -d
```
- Logged in at http://localhost:8081 with admin.

-[x] Connected GitHub repo
- Added repo containing Kubernetes manifests.
- Created an ArgoCD Application pointing to that repo.

-[x] Synced Application
- Clicked Sync in ArgoCD UI.
- Jenkins pods deployed into Minikube cluster.

- [x] Verified with:
```bash
kubectl get pods -n jenkins
```



