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
    - CLI commands
        - create resource group: `az group create --name [RG name] --location [location]`
        - create VM: `az vm create --resource-group [RG name] --name [VM name] --image [image name] --admin-username [user name]`
            - when this command is run, you'll be prompted for a password
    - PowerShell commands
        - create resource group: `New-AzResourceGroup -Name new-vm-grp -Location EastUS`
        - create VM: `New-AzVm -ResourceGroupName "new-vm-grp" -Name "demovm1" -Location "East US" -VirtualNetworkName "demo-network" -SubnetName "subnetA" -SecurityGroupName "myNSG" -PublicIpAddressName "new-ip" -OpenPorts 80,3389`
- Azure backup service for VMs
    - data is backed up to Recovery Services vault, which is a resource in the same region as the VM
    - only backs up changes since the last backup
    - backup policy sets frequency, how long you want the data backed up for and which recovery points you always want to keep (let's say, the recovery point exactly a year ago)
    - recovery points are created with every backup
    - you can choose to recover certain files, the entire VM or a disk
    - types of snapshots
        - application consistent: backs everything up, including pending I/O operations
        - file-system consistent: backups up all the files at the same time
        - crash consistent: happens if the VM shuts down during the backup

### Section 4: Develop Azure compute solutions - Azure Web Apps and Azure Functions
- Azure Web App Service
    - supported languages: .NET, .NET Core, Java, Python, Node.js, Ruby
    - it's a PaaS, you don't manage the VM/DBs your app runs on
    - it has scaling
    - high security
    - DevOps capabilities like continuous deployment
- App Service Plan
    - your app lives on an App Service Plan (which is a resource)
    - free: 10 apps, 1GB disk space, 60 CPU minutes/day
    - shared: 100 apps, 1GB, 240 CPU minutes/day
    - basic: unlimited apps, 10GB, unlimited CPU minutes/day, 3 maximum instances
        - maximum instances: the number of VMs you can have on the plan to run your apps, the requests get balanced between the instances
    - all web apps on a plan have to be in the same region as the plan
    - all web apps on a plan have to have the same underlying OS
- Azure Web App logging
    - types of logging
        - app logging: logs generated by your app
        - web server logging: records HTTP requests
        - detailed error messages: stores .htm error pages that would've gone to the client
        - deployment logging: errors that occur during publish
    - logs are streamed in real time
    - you can access the stream through an FTP URL of from the log stream page on your web app resource
- you can enable continuous deployment with GitHub Actions by linking your web app to a GitHub repo
    - if you link your web app to a GitHub repo, continuous deployment will be automatically implemented
- Web App CLI commands
    - `$plan="plan-name"`
    - `$appname="app-name"`
    - `$repoulr="https://github.com/[username]/[repo name]"`
    - `az group create --location westeurope --name [group name]`
    - `az appservice plan create --name $plan --resource-group [group name] --sku B1`
    - `az webapp create --name $appname --resource-group [group name] --plan $plan`
    - `az webapp deployment source config --name $appname --resource-group [group name] --repo-url $repourl --branch master --manual-integration`
    - `manual-integration`: you have to trigger a deployment, no continuous deployment on code change
- custom domain
    - buy a domain name
    - go to the custom domains page on the web app resource and add custom domain
    - set the custom domain to the name you bought and save the custom domain 
    - on the domain provider site you have to have a CNAME record that links your original web app URL (that Azure assigns) to your new domain
    - SSL custom domain
        - go to TLS/SSL settings and create an app service managed certificate
        - add SSL binding (new certificate to custom domain)


### Section 5: Develop Azure compute solutions - Docker, Azure Container Instances, Kubernetes

### Section 6: Develop for Azure Storage

### Section 7: Implement Azure Security

### Section 8: Monitor, troubleshoot, and optimize solutions

### Section 9: Connect to and consume Azure and third-party services
