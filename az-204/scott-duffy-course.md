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
- Durable Functions
    - stateful
    - long-running tasks (more than 30min)
    - can be suspended while it waits for another call to complete
    - can call other functions
    - can make async calls
    - made up of
        - client: the original function that gets triggered, generally starts the orchestrator
        - orchestrator: the traffic cop, makes sure the activities run in the right order
        - activity: basic unit of work in a function
- how to set up durable functions
    - create an app service plan
    - go to App Service Editor
    - create a package.json file in the app service root
    - add app name and version to the file
    - use npm to install durable functions package
        - `npm install durable-functions`
    - you can now create a function based on the durable function starter template
    - then create a function based on the durable function orchestrator template
        - it references the activity functions
    - then create functions for each activity, based on the durable function activity template
    - test the durable function by calling the starter/client function
        - it returns several URLs that can give you back different information about the durable function and its state
- delays and timers
    - install TypeScript and Moment from the App Service Plan's console
    - add `const moment = require('moment');` to the orchestrator function
    - `deadline = moment.utc(context.df.currentUtcDateTime).add(1, 'h');`
    - `yield context.df.createTimer(deadline.toDate());`
    - `outputs.push(yield context.df.callActivity('ActivityFunctionName', 'parameter/s'));`
- Function Core Tools - func
    - you can create functions in the cloud shell
    - `func init` + `func new` and then `code .` to open a code editor
    - `func start` runs the function on localhost in the cloud shell
    -  then you can `az functionapp create` to create a function app
    - `func azure functionapp publish "name of function app"` to publish the function to a function app
- custom handlers
    - use programming languages that aren't traditionally supported by Azure function apps
    - choose "Custom Handler" for runtime stack on the create function app screen
    - you have to develop the app in a code editor that supports your language
    - in host.json you
        - set the `customHandler.description/defaultExecutablePath` to `handler` (or `handler.exe` for Windows)
        - set `customHandler/enableForwardingHttpRequest` to `true`
        - the handler will be the complied function code

### Azure storage accounts
- unmanaged storage accounts are the ones you create as resources for whatever you want
    - premium performance tier
        - you pay more per GB of storage but less for the transactions themselves
        - used for data you're accessing hundreds of times a second
    - in the networking tab, when creating a storage account, you can choose
        - access the account through a public endpoint
            - you'd still need a private access key to hit the endpoint
        - access the account through a specific network, and then you pick/create a virtual network
        - a private endpoint cannot be accessed from the internet, even with an access key or via VPN
    - blob containers
        - types of containers
            - private: no anonymous read access
            - blob: anonymous read access for blobs
            - container: anonymous read access for entire container
    - accessing data from storage account
        - under the storage account's properties, there is a URL for each of the service types (blob, file, queue, table, Data Lake, static website)
            - if you have read-only geo-redundant storage enabled, you get a secondary endpoint for each type as well
        - under access keys you will find the access keys that enable full access to the emtire account
            - hitting the endpoint for a file or account/service with the key will serve you the file/account/service
        - under shared access signature (SAS) you can select permissions and a time duration that the files/services can be accesses and then generate a token that can be appended to the endpoint URLs
- managed storage accounts are the accounts Azure makes when you create a VM, open the cloud shell for the first time, etc., you don't create them directly

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


