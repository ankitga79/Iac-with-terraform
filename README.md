# Terraform Project: Provision Docker Container

## 📌 Overview
This project uses **Terraform** to provision a **Docker container** running an **NGINX server** on your local machine.

## 🛠️ Prerequisites
Before running this project, ensure you have the following installed:

- **Terraform**
- **Docker**
- **Linux Ubuntu**

## 📂 Project Structure
```
my-terraform-project/
│── main.tf    # Terraform configuration file
│── README.md  # Documentation file
```

## ⚙️ Terraform Configuration (`main.tf`)
```hcl
provider "docker" {}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}

resource "docker_container" "nginx_container" {
  image = docker_image.nginx.image_id
  name  = "my_nginx"
  ports {
    internal = 80
    external = 8080  # Change if port is in use
  }
}
```

## 🚀 Usage
### **1️⃣ Initialize Terraform**
Run the following command to initialize Terraform:
```sh
terraform init
```

### **2️⃣ Check Execution Plan**
Before applying changes, check what Terraform will do:
```sh
terraform plan
```

### **3️⃣ Apply Configuration**
Deploy the container:
```sh
terraform apply -auto-approve
```

### **4️⃣ Verify the Container**
Check if the container is running:
```sh
docker ps
```
Visit [http://localhost:8080](http://localhost:8080) in your browser.

### **5️⃣ Destroy Infrastructure**
To remove the container and free up resources:
```sh
terraform destroy -auto-approve
```

## 🛠 Troubleshooting
### **Port 8080 Already in Use?**
Check which process is using it:
```sh
sudo netstat -tulnp | grep :8080
```
Kill the process (replace `<PID>` with the actual process ID):
```sh
sudo kill -9 <PID>
```

Alternatively, update `main.tf` to use a different port (e.g., **8081** instead of **8080**).

### **Check Running Containers**
```sh
docker ps -a
```

