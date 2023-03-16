# jenkins-docker-compose-setup
jenkins-docker-compose-setup

# Run using only docker
```
docker container run -d \
    -p [YOUR PORT]:8080 \
    -v [YOUR VOLUME]:/var/jenkins_home \
    --name jenkins-local \
    jenkins/jenkins:lts
    
 -p: assign port target
 -v: attach volume
 -d: detached mode
 --name: named container
 --restart=on-failure

docker container run -d -p 8081:8080 -p 50000:50000 \
    -v jenkins:/var/jenkins_home \
    --name jenkins-local \
    --restart=on-failure \
    jenkins/jenkins:lts
```

# Install docker-compose:
Instructions url: 
```
https://docs.docker.com/compose/install/
```

# Create folders: 
```
mkdir -p jenkins-configuration
mkdir ~/jenkins
```

# Create docker-compose file:
```
vim docker-compose.yaml
```

# Add the following content to file:
```
version: '3.7'
services:
  jenkins:
    image: jenkins/jenkins:lts
    privileged: true
    user: root
    ports:
      - 8081:8080
      - 50000:50000
    container_name: jenkins
    volumes:
      - ~/jenkins:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock
      - /usr/local/bin/docker:/usr/local/bin/docker
```

# Login:
```
 localhost:8081
```

# Get admin password:
```
 docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```
# An Example pipeline:
```
pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
```
