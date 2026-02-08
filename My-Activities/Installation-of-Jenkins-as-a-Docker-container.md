## Installation as a Docker container

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
