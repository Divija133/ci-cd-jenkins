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
- [x]Configured jobs to run Docker builds using the mounted socket.

7.
