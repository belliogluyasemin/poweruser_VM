
# poweruser_VM

In this project, a virtual machine (VM) was created. After the VM creation, an SSH connection was established to this VM. Following the SSH steps, the interface was accessed through the IP address. The steps below detail this process:

1. **VM Creation**: Initially, an Ubuntu VM was created with the necessary configurations and settings.
2. **SSH Connection**: An SSH connection was established to the created VM using the command:
   ```sh
   ssh username@VM_IP_address

3.Docker Image Setup: The Docker image previously uploaded to Docker Hub was pulled into this VM and run. The necessary SSH commands are as follows:

    -sudo apt update
    -sudo apt upgrade
    -sudo ps
    -sudo apt install docker.io
    -sudo docker login
    # Enter Docker Hub credentials
    -Login Succeeded
    -sudo docker pull yaseminbellioglu/xgboost_adasyn_poweruser_image:v1
    -sudo docker run -d -p 80:8000 yaseminbellioglu/xgboost_adasyn_poweruser_image:v1
    -sudo docker images
    -sudo docker ps
    -sudo docker stop busy_cohen
    -sudo docker rmi 1180993f1653

4-Accessing the API: As shown in the fastApi_VM.png file, the API can be accessed by connecting to the machine via the External IP Address.






