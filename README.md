AccuKnox QA Engineer Practical Assessment – Sindhu Mattegunta

Problem Statement 1:

Project Repository: https://github.com/Vengatesh-m/qa-test

Question 

Kubernetes Deployment:
● Deploy the services given in the above-mentioned repository to a local
Kubernetes cluster (e.g., Minikube or Kind).

Verification:
● Ensure the frontend service can successfully communicate with the backend service.
● Verify that accessing the frontend URL displays the greeting message
fetched from the backend.
Setup, Execution Instructions and Output
I have deployed your frontend and backend services and built and pushed the Docker images to Docker Hub. Now, frontend service is accessible at http://127.0.0.1:49214 due to the Minikube tunnel.
Setup and Execution Instructions
Step 1: Minikube is running and Docker also running
Step 2: Start Minikube
Step 3: Clone the Repository
Step 4: Services cloned in Directory
Step 5: Deployed the Backend and Frontend to Kubernetes:
Step 6: Verified Deployments and Services:
Step 7: Build Docker Images:
Step 8: Frontend Docker images
Step 9: Backend Docker images and Images created in Docker
Step 10: Pushed Docker Images to Docker Hub and Can see images pushed to docker hub
Step 11: Access the Frontend Service
Final Output
The frontend service will be accessible at http://127.0.0.1:49214.
You can see the output with the URL  http://127.0.0.1:49214
Summary
Here’s a summary of the main commands:
•	minikube start
•	git clone https://github.com/Vengatesh-m/qa-test
•	cd qa-test
•	cd Deployment
•	kubectl apply -f backend-deployment.yaml
•	kubectl apply -f frontend-deployment.yaml
•	kubectl get pods
•	kubectl get services
•	cd ../frontend
•	docker build -t sindhu1989/frontend:latest .
•	cd ../backend
•	docker build -t sindhu1989/backend:latest .
•	docker push sindhu1989/frontend:latest
•	docker push sindhu1989/backend:latest
•	minikube service frontend-service
Question
Automated Testing:
● Write a simple test script (using a tool of your choice) to verify the
integration between the frontend and backend services.
● The test should check that the frontend correctly displays the message returned by the backend.

Test Script on Bash

# Save the following content into a file named test_integration.sh

#!/bin/bash

# URL of the frontend service
FRONTEND_URL=http://127.0.0.1:49214

# Fetch the frontend page
RESPONSE=$(curl -s $FRONTEND_URL)

# Expected message
EXPECTED_MESSAGE="Hello from the backend!"

# Check if the response contains the expected message
if echo "$RESPONSE" | grep -q "$EXPECTED_MESSAGE"; then
  echo "Test Passed: Frontend displays the correct message from the backend."
  exit 0
else
  echo "Test Failed: Frontend does not display the correct message from the backend."
  exit 1
fi

Problem Statement 2:

1. System Health Monitoring Script: I have attempted to achieve with Bash
Develop a script that monitors the health of a Linux system. It should check
CPU usage, memory usage, disk space, and running processes. If any of
these metrics exceed predefined thresholds (e.g., CPU usage > 80%), the
script should send an alert to the console or a log file.

System Health Monitoring Script
This script will monitor CPU usage, memory usage, disk space, and running processes. If any of these metrics exceed predefined thresholds, it will send an alert to the console.
Test Script in Bash

#!/bin/bash

# Thresholds
CPU_THRESHOLD=80
MEMORY_THRESHOLD=80
DISK_THRESHOLD=90

# Log file
LOG_FILE="/var/log/system_health.log"

# Function to check CPU usage
check_cpu_usage() {
  CPU_USAGE=$(top -bn1 | grep "Cpu(s)" | \
             sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | \
             awk '{print 100 - $1}')
  echo "CPU Usage: $CPU_USAGE%"
  if (( ${CPU_USAGE%.*} > CPU_THRESHOLD )); then
    echo "ALERT: CPU usage is above $CPU_THRESHOLD%" | tee -a $LOG_FILE
  fi
}

# Function to check memory usage
check_memory_usage() {
  MEMORY_USAGE=$(free | grep Mem | awk '{print $3/$2 * 100.0}')
  echo "Memory Usage: $MEMORY_USAGE%"
  if (( ${MEMORY_USAGE%.*} > MEMORY_THRESHOLD )); then
    echo "ALERT: Memory usage is above $MEMORY_THRESHOLD%" | tee -a $LOG_FILE
  fi
}


# Function to check disk space usage
check_disk_space() {
  DISK_USAGE=$(df -h / | grep / | awk '{ print $5 }' | sed 's/%//g')
  echo "Disk Usage: $DISK_USAGE%"
  if (( DISK_USAGE > DISK_THRESHOLD )); then
    echo "ALERT: Disk usage is above $DISK_THRESHOLD%" | tee -a $LOG_FILE
  fi
}

# Function to check running processes
check_running_processes() {
  RUNNING_PROCESSES=$(ps aux --no-heading | wc -l)
  echo "Running Processes: $RUNNING_PROCESSES"
}


2. Automated Backup Solution:
Write a script to automate the backup of a specified directory to a remote
server or a cloud storage solution. The script should provide a report on the
success or failure of the backup operation.

Test Script in Bash

#!/bin/bash

# Variables 
SOURCE_DIR="/path/to/source/directory"
REMOTE_USER="remote-user"
REMOTE_HOST="remote-host"
REMOTE_DIR="/path/to/remote/directory"
LOG_FILE="/var/log/backup.log"

# Function to perform the backup
perform_backup() {
  rsync -avz --delete $SOURCE_DIR $REMOTE_USER@$REMOTE_HOST:$REMOTE_DIR
  if [[ $? -eq 0 ]]; then
    echo "$(date) - Backup successful" | tee -a $LOG_FILE
  else
    echo "$(date) - Backup failed" | tee -a $LOG_FILE
  fi
}
















