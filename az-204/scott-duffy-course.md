### virtual machines
- Azure spot instance: you get to rent for cheap a VM for a short time (less than a day)
- after choosing options for the VM you can save those settings as an ARM template
- resources created with a VM
    - VM itself
    - public IP address
    - virtual network card
    - network security group
    - virtual network (in the same region as the VM)
    - virtual disk/s
    - optional resources
        - automatic shutdown rule
        - etc.
- ARM templates
    - creating a VM from an ARM template gives you a form with inputs for the parameters in the template script
    - you can save the parameters JSON file from a deployed VM and import the JSON into the template form
    - admin user password doesn't get saved/imported as a parameter

### Azure App Service
- a web app lives inside an app service plan
- ACU: Azure compute unit
- WebJobs
    - a background task that is attached to a web app
    - it runs on a schedule
    - kind of like a timer-triggered Azure Function
- deployment slots
    - a way to host multiple instances of an app all under one web app instance
- CLI hint: use `get-command *{search term}*` to search for a command
- Kudu
    - when you publish your web app, you get a URL for the Kudu site of your app
    - the Kudu site gives you details about your app
        - files
        - log streams
        - deployment scripts
    - from the site you can use a cloud Bash or PowerShell shell to navigate the directories

### containers
- Azure offers different container options
    - you can pick to deploy your web app to a Docker container when you create the app resource
    - you can create a Kubernetes resource, which is complex to set up and use, but it's powerful and scales well
    - you can create an Azure container instance, which is a simple and fast way to get a container running, but it's not as powerful as Kubernetes and it doesn't scale
- you can build your web app project into an image and push it to a directory right from VS
- you can then deploy those images to an Azure web app, a VM with Docker running on it, an Azure Container Instance, etc.
- Docker image: a bundle of OS, dependencies and code that can be used to create and run a container instance
- Azure Container Registry
    - a place to publish private container images
    - DockerHub, on the other hand, is a public registry
    - a container registry is a resource
- Azure Container Instance
    - a container instance is a resource in which a deployed container image runs
    - ACI is faster to deploy than an app service, but app services have more features (backups, scaling, etc.)

### Function App


### Azure storage accounts


### CosmosDB


### SQL database


### blob containers


### Azure authentication


### Azure Access Control


### secure data


### scaling apps and services


### caching and content delivery networks


### monitoring and logging


### consuming Azure services


### application messaging


