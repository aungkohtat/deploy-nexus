
# Nexus Repository Installation

## Environment

- **Platform**: DigitalOcean Droplet (Ubuntu)
- **Privileges**: Root SSH access
- **Component**: Sonatype Nexus Repository 3 via Docker

## Step-by-Step Progress

### 1. Preparing the Droplet

- Provisioned a new **Ubuntu droplet** on DigitalOcean.
- Obtained **root SSH access** for setup and installation.

### 2. Docker Installation

```
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install -y docker-ce
```

- Confirmed Docker is running with:
  
Documentation

```
sudo systemctl status docker

```


### 3. Docker Verification


```
docker --version
sudo systemctl status docker
```

### 4. Persistent Data Storage

```

docker volume create nexus-data

```
*or*  
```

mkdir -p /opt/nexus-data
chmod -R 200 /opt/nexus-data

```

### 5. Nexus Repository Container Deployment

```

docker pull sonatype/nexus3
docker run -d -p 8081:8081 --name nexus \
  -v nexus-/nexus-data \
  sonatype/nexus3

```
*or with directory binding:*
```

docker run -d -p 8081:8081 --name nexus \
  -v /opt/nexus-/nexus-data \
  sonatype/nexus3

```
- Verified the container is running:
```

docker ps

```

### 6. Web Access and Initial Setup

- Make sure port **8081** is open.
- Access Nexus Web UI at:  
  `http://<your_droplet_ip>:8081`
- Retrieve the initial admin password:
```

docker exec nexus cat /nexus-data/admin.password

```
- Log in as `admin` with the obtained password.

## Troubleshooting and Corrections

- Faced Docker daemon error, fixed with:
```

sudo systemctl start docker

```
- Checked permissions and environment variables.

## Current Status

- **Nexus Repository is running and accessible.**
- Data is persisted in Docker volume.
- Ready for use.

**References:**  
- [Nexus Docker Image Documentation]

*Replace `<your_droplet_ip>` with your actual droplet IP address.*
```
http://128.199.176.24:8081/
```

