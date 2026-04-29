# Spring Boot based Java web application
 
This is a simple Sprint Boot based Java application that can be built using Maven. Sprint Boot dependencies are handled using the pom.xml 
at the root directory of the repository.

This is a MVC architecture based application where controller returns a page with title and message attributes to the view.

## Execute the application locally and access it using your browser

Checkout the repo and move to the directory

```
git clone https://github.com/iam-veeramalla/Jenkins-Zero-To-Hero/java-maven-sonar-argocd-helm-k8s/sprint-boot-app
cd java-maven-sonar-argocd-helm-k8s/sprint-boot-app
```

Execute the Maven targets to generate the artifacts  -> Don't perform this step, please follow the docker way, its easy

```
mvn clean package
```

The above maven target stroes the artifacts to the `target` directory. You can either execute the artifact on your local machine
(or) run it as a Docker container.

** Note: To avoid issues with local setup, Java versions and other dependencies, I would recommend the docker way. **


### Execute locally (Java 11 needed) and access the application on http://localhost:8080

```
java -jar target/spring-boot-web.jar
```

### The Docker way

Build the Docker Image

```
docker build -t ultimate-cicd-pipeline:v1 .
```

```
docker run -d -p 8010:8080 -t ultimate-cicd-pipeline:v1
```

Hurray !! Access the application on `http://<ip-address>:8010`


## Next Steps

### Configure a Sonar Server locally

```
System Requirements
Java 17+ (Oracle JDK, OpenJDK, or AdoptOpenJDK)
Hardware Recommendations:
   Minimum 2 GB RAM
   2 CPU cores
sudo apt update && sudo apt install unzip -y
adduser sonarqube
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-10.4.1.88267.zip
unzip *
chown -R sonarqube:sonarqube /opt/sonarqube
chmod -R 775 /opt/sonarqube
cd /opt/sonarqube/bin/linux-x86-64
./sonar.sh start
```

Hurray !! Now you can access the `SonarQube Server` on `http://<ip-address>:9000` 

- Credentials of Sonarqube is `username: admin` and `password: admin`
- Generate the token in Sonarqube, so that `Jenkins` can able to authenticate with `Sonarqube`
     - Sonarqube --> Myaccount --> Security --> Generate Token(give any name) and generate it
     - Jenkins --> Manage Jenkins --> Manage Creds --> global creds -->

       <img width="1914" height="1014" alt="image" src="https://github.com/user-attachments/assets/ca3fe15b-b51c-4410-838b-e85411593a7b" />


### Install the Docker on EC2
- Follow the root repo

### Start the minikube cluster on your lap

```
minikube start --memory=4098 --driver=hyperkit
```

### Install the ArgoCD controller in minikube

- We are going to install this controller using ArgoCD Operator
- Kubernetes operators will manage the lifecycle of kubernetes controller
- Search for ArgoCD and install it [operatorhub.io](https://operatorhub.io/)

  <img width="1919" height="990" alt="image" src="https://github.com/user-attachments/assets/f1f5297e-4fc0-4668-9850-66edb065d2ba" />

- Edit the service to `NodePort` from `ClusterIP` ( `kubectl edit service example-argocd-server`)
- List the service (`minikube service list`), through browser we can access the URL
- `username`: admin, `password`: take from `kubectl edit secret example-argocd-cluster `
- `echo -n cflyqn= | base64 -d`  -> Decode the password

### Configure creds for Git and docker in Jenkins
- Use manage Jenkins -> credentials option. we need a token from git and docker.

 <img width="1906" height="663" alt="image" src="https://github.com/user-attachments/assets/fc562d3b-f834-47b0-8c24-e1499a77f66b" />

### Try to build manually 

- Click build now in Jenkins, it should get success

