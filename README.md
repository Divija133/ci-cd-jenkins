# ci-cd-jenkins

1. Update Package Index

Ensured Linux environment has the latest package lists.

``` bash
sudo apt-get update
sudo apt-get upgrade -y
```

2.Install Required Packages

Installed dependencies needed for Docker to run.

```bash
sudo apt-get install -y ca-certificates curl gnupg lsb-release
```

3.Add Docker’s Official GPG Key

Ensured package authenticity.

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

4.Set Up Docker Repository

Added Docker’s stable repository to apt sources.

```bash
echo \"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable\" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

5.Install Docker Engine

Installed Docker CE, CLI, and containerd.

```bash
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

6.Verify Installation

Confirmed Docker is installed and running.

```bash
docker --version
sudo service docker start
```
