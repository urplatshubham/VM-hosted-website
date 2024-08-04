### Hosting a Website in a VM and Scanning with Nmap in the Host Machine

---

#### Introduction

This guide walks you through the process of hosting a website on a virtual machine (VM) and scanning the VM from the host machine using Nmap. You'll learn how to configure your VM, deploy a website, and ensure network security by checking open ports.

##### In this example I have used Oracle Virtual Machine to configure my VM using ubuntu 22.04 image downloaded from [official osboxes website](http://osboxes.org)
---

#### Features

- Host a website on a VM using Nginx.
- Scan the VM from the host machine using Nmap.
- Check for open ports and running services.
- Ensure secure configuration of network services.

---

#### Prerequisites

- A host machine running Windows, Linux, or macOS.
- A VM running a Linux distribution.
- Internet connection.
- Basic knowledge of networking and Linux command line.

---

#### Installation

1. **Install Nmap on the Host Machine:**
   - **Linux:**
     ```sh
     sudo apt-get install nmap
     ```
   - **macOS (via Homebrew):**
     ```sh
     brew install nmap
     ```
   - **Windows:** Download and install from the [official Nmap website](https://nmap.org/download.html).

2. **Set Up the VM:**
   - Install a Linux distribution on your VM (e.g., Ubuntu).
   - Ensure the VM is connected to the network and can access the internet.
   - How to Install VirtualBox 

Here's a step-by-step guide to installing Oracle VirtualBox on your Windows, macOS, or Linux computer: 

   - Step 1: Download VirtualBox 
   - Go to the official VirtualBox website: https://www.virtualbox.org/ 
   - Click on the "Downloads" link in the top navigation menu. 
   - Choose the Correct Package 
   - On the Downloads page, you'll see various packages for different host operating   systems. Select the appropriate package for your OS (e.g., Windows, macOS, or Linux). 

Install VirtualBox

- For Windows: 

    - Download the installer for Windows and double-click on the downloaded file to start the installation. 

    - Follow the on-screen instructions and accept the license agreement. - Choose the components you want to install and the installation path. - Complete the installation process. 

- For macOS: 

    - Download the macOS version of VirtualBox. 

    - Double-click on the downloaded DMG file to open it. 

    - Double-click on the VirtualBox package icon to start the installation. - Follow the on-screen instructions to complete the installation. 

- For Linux: 

    - Download the appropriate package for your Linux distribution (e.g., .deb for Debian/Ubuntu-based systems, .rpm for Red Hat/Fedora-based systems). - Install VirtualBox using the package manager of your Linux distribution. For example, for Ubuntu, use the following command in the terminal: 
        ```sh
        sudo dpkg -i <VirtualBox_package_name>.deb 
        ```

    - You may need to install additional dependencies if prompted by the package manager. 

- Post-installation Configuration (All Operating Systems) 

    After installation, you might need to add your user account to the "vboxusers" group (Linux) or "VirtualBox Users" group (Windows) to grant permissions to manage VMs. 

- Launch VirtualBox 

  Once the installation is complete, you can launch VirtualBox from your application menu (Windows and Linux) or from the Applications folder (macOS). 

```sh
Congratulations! You now have Oracle VirtualBox installed on your computer and can start creating and managing virtual machines for various purposes, including development, testing, and exploration of different operating systems.
```
---

#### Configuration

1. **Configure Nginx on the VM:**
   - Install Nginx:
     ```sh
     sudo apt-get update
     sudo apt-get install nginx
     ```
   - Start Nginx:
     ```sh
     sudo systemctl start nginx
     sudo systemctl enable nginx
     ```

2. **Deploy a Simple Website:**

   - Create the Website Directory:
     ```sh
     sudo mkdir -p /var/www/ubuntuAwesomeWeb
     ```   
     Create an HTML file:
     ```sh
     sudo nano /var/www/ubuntuAwesomeWeb/index.html
     ```
     Add the following content: (The below example is a sample HTML file)
     ```sh
    
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <title>Awesome Web</title>
        </head>
        <body>
            <h1>Welcome to Ubunbtu Awesome Web!</h1>
            <p>This is a simple HTML page hosted with Nginx.</p>
        </body>
        </html>
     ```
   - Configure Nginx to serve the website:
     ```sh
     sudo nano /etc/nginx/sites-available/ubuntuAwesomeWeb
     ```
     Add the following configuration:
     ```
     server {
         listen 80;
         server_name awesomeweb;

         root /var/www/html;
         index index.html;

         location / {
             try_files $uri $uri/ =404;
         }
     }
     ```
   - Enable the configuration:
     ```sh
     sudo ln -s /etc/nginx/sites-available/ubuntuAwesomeWeb /etc/nginx/sites-enabled/
     sudo systemctl restart nginx
     ```

---

#### Usage

1. **Access the Website:**
   - In your web browser, navigate to the VM's IP address (e.g., this is my VM's IP address `http://172.18.0.1`).
   - You should see the "Welcome to Ubuntu Awesome Web" message.

2. **Scan the VM from the Host Machine:**
   - Identify the VM's IP address using `ifconfig` or `ipconfig`.
   - Run an Nmap scan:
     ```sh
     nmap -sS -p 80,443,22 172.18.0.1 (this requires root access)
     ```
     Alternatively you can also try:
     ```sh
     nmap -sV 172.18.0.1 
     ```

---

#### Testing

1. **Verify Website Access:**
   - Open a web browser and navigate to `http://172.18.0.1`.
   - Ensure the webpage loads correctly.

2. **Verify Nmap Scan:**
   - Run the Nmap scan and check the output.
   - Ensure the expected ports (80, 443, 22) are open.

---

#### Troubleshooting

- **Website Not Loading:**
  - Check Nginx status: `sudo systemctl status nginx`
  - Verify VM network settings.
- **Nmap Scan Not Showing Open Ports:**
  - Ensure VM firewall is not blocking ports: `sudo ufw status`
  - Confirm Nginx is running on the VM.

---

#### Contributing

Contributions are welcome! Please open an issue or submit a pull request on the GitHub repository.

---

#### License

This project is licensed under the MIT License. See the LICENSE file for details.

---

#### Contact

For questions or support, please contact [imperialshubham.3@gmail.com].

---
