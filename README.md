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






Docker file for .war 
FROM tomcat:9-jdk11
COPY **/*.war /usr/local/tomcat/webapps
EXPOSE 8080
CMD ["catalina.sh","run"]
