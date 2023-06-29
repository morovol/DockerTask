# DockerTask
1.	Deploy the docker environment on a working machine.  
2.	Deploy Keycloak, Jenkins, SonarQube using docker containers. Keycloak should work on port 8432. Jenkins should work on port 8332. SonarQube should work on port 9000.  
3.	Deploy Keycloak with PostgreSQL database.  
4.	Display detailed information for each containers.  
5.	Create Jenkins agent according to requirements:  
-	as a basic image use openshift/jenkins-slave-base-centos7:v3.11  
-	update java version to 11  
-	install kubectl  
-	install helm 3  
-	install helm-push plugin  
-	install hadolint  
-	install tfenv  
-	the generated Dockerfile must pass the hadolint check  
-	upload the resulting docker image to the docker hub  
as a result of work, provide a Dockerfile.

# Implementation
1. Installed Docker  
2,3. Created docker-compose.yaml  
4. Docker inspect <id_container>  
5. Create Dockerfile  
- docker build -t <name_image>:<tag>  
- docker push  
- hadolint <dockerfile_path>  
