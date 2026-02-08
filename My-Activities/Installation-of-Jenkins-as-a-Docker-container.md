## Installation as a Docker container

## Method 1

```bash
# Pull the image
docker pull jenkins/jenkins:lts

# Make sure E:\ubuntu-data\Jenkins exists
docker run -d --name Jenkins-container -p 9080:8080 -p 50000:50000 -v E:\ubuntu-data\Jenkins:/var/jenkins_home jenkins/jenkins:lts

# Login to the container and take the initial password
jenkins@510555411f0f:/$ cat /var/jenkins_home/secrets/initialAdminPassword
43d92480645d45df9962b1220186e4c9

# Then you can do inital steps like creating username,password,full-name,email-address

# Access using below url
http://localhost:9080/
```

## Method 2

Follow the official [doc](https://www.jenkins.io/doc/book/installing/docker/#on-windows), modify commands accoriding to powershell like below

```bash
# Run Docker-in-Docker (DinD)
docker run --name jenkins-docker --rm --detach `
  --privileged --network jenkins --network-alias docker `
  --env DOCKER_TLS_CERTDIR=/certs `
  --volume jenkins-docker-certs:/certs/client `
  --volume jenkins-data:/var/jenkins_home `
  --publish 2376:2376 `
  docker:dind

# Run Jenkins BlueOcean
docker run --name jenkins-blueocean --restart=on-failure --detach `
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 `
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 `
  --volume jenkins-data:/var/jenkins_home `
  --volume jenkins-docker-certs:/certs/client:ro `
  --publish 9092:8080 --publish 50000:50000 myjenkins-blueocean:2.541.1-1

```
