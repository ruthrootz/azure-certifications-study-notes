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

### Section 4: Develop Azure compute solutions - Azure Web Apps and Azure Functions

### Section 5: Develop Azure compute solutions - Docker, Azure Container Instances, Kubernetes

### Section 6: Develop for Azure Storage

### Section 7: Implement Azure Security

### Section 8: Monitor, troubleshoot, and optimize solutions

### Section 9: Connect to and consume Azure and third-party services
