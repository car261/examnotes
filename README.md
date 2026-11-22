# examnotes

mvn clean package
 Dockerfile 
 FROM tomcat:9.0
COPY target/*.war /usr/local/tomcat/webapps/
EXPOSE 7070
CMD ["catalina.sh","run"]

docker build -t exam .

minikube start

minikube image load exam:latest

deployment.yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: vehicle-rental
spec:
  replicas: 2
  selector:
    matchLabels:
      app: vehicle-rental
  template:
    metadata:
      labels:
        app: vehicle-rental
    spec:
      containers:
        - name: vehicle-rental
          image: exam:latest
          imagePullPolicy: Never
          ports:
            - containerPort: 8080


kubectl apply -f deployment.yaml
kubectl port-forward deployment/vehicle-rental 8888:8080
http://localhost:8888/CampusMgmtSystem/

# Use an official Java runtime as a parent image
FROM tomcat:9-jdk11

# Copy the built WAR file to the Tomcat webapps directory
COPY target/*.war /usr/local/tomcat/webapps/

# Expose the port Tomcat is running on
EXPOSE 8080

# Start Tomcat server
CMD ["catalina.sh", "run"]







sudo + ..........
Step 1:- build your image
docker build –t <imagename> .(dot)
Step 2:- check for images
Step 3:- run image
docker run –d --name app-demo –p 6060:8080 <image name>


Docker file for .war 
FROM tomcat:9-jdk11
COPY **/*.war /usr/local/tomcat/webapps
EXPOSE 8080
CMD ["catalina.sh","run"]
