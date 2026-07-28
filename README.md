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

- [x] stored secrets in Jenkins Credentials → referenced them by ID in Jenkinsfile → Jenkins injected them securely during pipeline execution.

   
