# Hosting a Django Project with Docker and Nginx 🚀

### 1. Update the Server  
Before setting up Docker and deploying your Django project, ensure your server is up to date by running the following commands:  

```console
sudo apt update
sudo apt upgrade
```  

### 2. Install Docker Engine
To install Docker on your server, run the following commands:

```console
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER
newgrp docker
```

### 3.  Set Up Your Project Directory
Create a new directory for your project (we’ll use example as the project name), and set up the necessary files:

```console
mkdir example
cd example

touch build.sh
chmod +x build.sh
touch Dockerfile
touch docker-compose.yml
```

In this step, we’re creating a directory called example. Next, you’ll need to copy the build.sh, Dockerfile, and docker-compose.yml files from this repository into your newly created directory. These files are essential for building and deploying your Django project using Docker and Nginx.


### 4. Generate a Deploy Key
A deploy key allows your server to securely access a private repository. Run the following command to generate an SSH deploy key:

```console
ssh-keygen -t rsa -b 4096 -C "deploy-key" -f ./id_ed25519 -N ""
```

#### Explanation of the Flags:  
- `-t ed25519` → Uses Ed25519 (a modern and secure SSH key type).  
- `-C "deploy-key"` → Adds a label to identify this as a deploy key.  
- `-f ./id_ed25519` → Saves the key in the current directory as `id_ed25519`.  
- `-N ""` → Creates the key without a passphrase (needed for automated deployments).


#### Next Steps:
1. Copy the **public key** (`id_ed25519.pub`).  
2. Add it to your repository's **Deploy Keys** in GitHub/GitLab (**Settings → Deploy Keys → Add Key**).
3. Ensure the key has **read access** (or write if needed).

This ensures your server can pull code securely without requiring a password.
Your instructions are well-structured! Here’s a refined version with improved clarity and flow:  


### **5. Install and Configure Nginx**  
Nginx will serve as a reverse proxy to forward requests to your Django application running in Docker. Follow these steps to install and configure it:  

#### **Install Nginx**  
Run the following command to install Nginx:  

```console
sudo apt install nginx -y
```  

#### **Set Up Nginx Configuration**  
Remove the default site configuration and create a new one for your project:  

```console
sudo rm -rf /etc/nginx/sites-enabled/default
sudo touch /etc/nginx/sites-available/example.conf
sudo ln -s /etc/nginx/sites-available/example.conf /etc/nginx/sites-enabled
```  

#### **Configure Nginx for Django**  
Copy the contents of `example.conf` from this repository to:  

```console
/etc/nginx/sites-available/example.conf
```  

#### **Reload Nginx**  
Once the configuration file is in place, test and reload Nginx:  

```console
sudo nginx -t
sudo service nginx reload
```  

If `nginx -t` shows **no errors**, your configuration is correct, and Nginx will successfully reload.  

### 6. Build and Run the Django Project
Now that everything is set up, run the build.sh script to build and start your Django project with Docker:

```console
./build.sh
```

This script will set up the Docker containers, install dependencies, and run your Django application. Once the build is complete, your Django project will be up and running!

Here’s a concise conclusion you can add to wrap up the README:

### **Conclusion**  
Congratulations! 🎉 You’ve successfully hosted your Django project using Docker and Nginx. By following these steps, you've set up a scalable, containerized application with a reverse proxy for improved performance and security.

Now you can easily deploy, manage, and scale your Django project with Docker, while Nginx ensures efficient handling of web traffic.

Feel free to customize the setup to your needs, and happy coding! 🚀