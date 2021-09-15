# [AZ-204 Developing Solutions for Azure Certification 2021](https://www.udemy.com/course/exam-microsoft-azure-dev/)

### Section 3: Develop Azure compute solutions - Virtual Machines
- when VM is deployed, these are also created
    - virtual network
    - disk storage
    - network interface, which acts as a virtual NIC
    - public and private IP addresses
    - network security group, acts as a firewall for the VM
- hosting a .NET Core web app on a Windows VM
    - create VM
    - add a port 80 inbound NSG rule
    - go to the NI resource, IP Configurations, and disassociate the public IP from the NI
    - assign a DNS name to the IP address resource and set the IP address to static
    - go back to the NI and reassociate the public IP address
    - log into VM and set it up as an IIS web server
    - install Management Service and add an IIS Manager rule that enables connections on port 8172
    - add a port 8172 inbound NSG rule
    - install .NET Core X.X Hosting Bundle, where X.X is the .NET Core version of your web app
    - install Web Deploy (which allows an IIS server to deploy apps, I guess?)
    - create a .NET Core project, right-click on the project and click publish
    - create a publish profile, choosing the VM you created
    - publish the app!
- hosting a .NET Core web app on a Linux VM
    - you can use PUTTY to log into the VM
    - Kestrel web server
        - cross-platform server for .NET Core
        - it's what runs .NET Core apps on Linux machines/VMs (instead of IIS)
        - when running a Linux .NET Core project locally, you can run it either on IIS Express or Kestrel
    - you can also use NGINX
    - publish the project to a folder
    - copy the folder onto the VM (using WinSCP)
    - install the Core SDK on the VM
    - `wget https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb`
    `sudo dpkg -i packages-microsoft-prod.deb`
    `sudo apt-get update; \`
        `sudo apt-get install -y apt-transport-https && \`
        `sudo apt-get update && \`
        `sudo apt-get install -y dotnet-sdk-3.1`
- creating a custom VM image
    - start by creating a VM and installing on it all the software/code you want your VMs to have
    - use Sysprep to remove user data and generalize the VM
    - stop the VM
    - create an image using the capture button
    - creating the image is a destructive process
- Azure Resource Manager templates
    - it's a JSON script
    - can be used to create VMs, storage accounts, SQL DBs, etc.
    - there are ready-made templates on the Marketplace
    - you can set a dependsOn property for a resource in the JSON
- Azure CLI
    - you need a storage account to use Cloud Shell
    - 

### Section 4: Develop Azure compute solutions - Azure Web Apps and Azure Functions

### Section 5: Develop Azure compute solutions - Docker, Azure Container Instances, Kubernetes

### Section 6: Develop for Azure Storage

### Section 7: Implement Azure Security

### Section 8: Monitor, troubleshoot, and optimize solutions

### Section 9: Connect to and consume Azure and third-party services
