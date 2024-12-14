# Use the official Jenkins LTS image as the base
FROM jenkins/jenkins:lts

# Switch to root user to install additional tools
USER root

# Install Nano, Maven, Docker, and Nginx
RUN apt-get update && \
    apt-get install -y nano maven apt-transport-https ca-certificates curl gnupg lsb-release nginx && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null && \
    apt-get update && \
    apt-get install -y docker-ce docker-ce-cli containerd.io && \
    rm -rf /var/lib/apt/lists/*

# Add Jenkins user to the Docker group
RUN usermod -aG docker jenkins

# Expose Jenkins and Nginx ports
EXPOSE 8080 80

# Start Nginx and Jenkins
CMD service nginx start && jenkins.sh

#Docker build -t jenkins-custom-image:1.0 <Path of the dockerfile to execute>

# docker run --name jenkins-custom -d -p 7070:8080 -p 8081:80 -v /var/jenkins-data:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock jenkins-custom-image:1.0
