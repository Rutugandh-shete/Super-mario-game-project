# Super-mario-game-project
### Flow of project
**1.	Launch one instance for installation purpose**
**2.	Write Terraform script to create EKS cloud**
**3.	After creating EKS cloud run deployment and service yaml fil	es to run the project.**

### step-1
Launch one instance of ubuntu machine, instance type t2.medium and 30 Gib storage.!
![Screenshot 2024-11-26 173639](https://github.com/user-attachments/assets/4a0d256a-5a33-40d8-b1a7-957a6d720696)

### step-2
Update your system 
````
sudo apt update -y
````
### step-3
Install Docker 
````
sudo apt install docker.io
sudo systemctl start docker # To start Docker 
sudo usermod -aG docker ubuntu # This will add ubuntu to docker group 
newgrp docker # refresh 
docker --version
````
![Screenshot 2024-11-26 175106](https://github.com/user-attachments/assets/1475d5ab-04f4-46e9-9971-373a25106720)

### step-4
Install Terraform 
````
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common

wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null

gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update
sudo apt-get install terraform
terraform --version

````
![image](https://github.com/user-attachments/assets/467df929-2de5-48df-974f-e749e75dd520)
### step-5
Install aws cli
````
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
#Above command help to download aws-cli and name that zip file according to our convenience
sudo apt install unzip 
unzip awscliv2.zip
sudo ./aws/install
aws --version

````
![image](https://github.com/user-attachments/assets/647ec157-9051-450e-9c85-1af3db6e46ea)

### step-6
Download the latest release with the command: 
````
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
````
Validate the kubectl binary against the checksum file:
````
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
````
Install kubectl:
````
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
````
If you do not have root access on the target system, you can still install kubectl to the ~/.local/bin directory:
````
chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
````
````
kubectl version --client
````
![image](https://github.com/user-attachments/assets/f6536d01-94b0-4dfd-a86a-104dc9d879d3)

### step-7
Create role add all policies those are required for EKS cluster and attach it to instance
#### Policies
![image](https://github.com/user-attachments/assets/2c85df53-c2af-4487-894e-dfe29998d6d3)
#### Update role
![image](https://github.com/user-attachments/assets/f3119cdd-0f63-454f-8d48-5bece6c06f21)

### step-8
create s3 bucket for creating backend and creating remote .tfstate
![image](https://github.com/user-attachments/assets/2b14e2c5-e3fa-4f98-b921-04689ecf9d92)


