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
- WebJobs
    - a background task that is attached to a web app
    - it runs on a schedule
    - kind of like a timer-triggered Azure Function

### containers


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


