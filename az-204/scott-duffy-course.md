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
- managed storage accounts are the accounts Azure makes when you create a VM, open the cloud shell for the first time, etc., you don't create them directly
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
            - blob: anonymous read access for all the blobs
            - container: anonymous read access for entire container
    - accessing data from storage account
        - under the storage account's properties, there is a URL for each of the container types (blob, file, queue, table, Data Lake, static website)
            - if you have read-only geo-redundant storage enabled, you get a secondary endpoint for each type as well
        - under access keys you will find the access keys that enable full access to the entire account
            - hitting the endpoint for a file/account/container with the key will serve you the file/account/container
        - under shared access signature (SAS) you can select permissions and a time duration that the files/containers can be accesses and then generate a token that can be appended to the endpoint URLs

### CosmosDB
- no-SQL, non-relational DB
- Cosmos guarantees sub 10ms latency
- it is more expensive than an Azure Table Storage
- types of CosmosDB accounts
    - Core (SQL)
        - JSON documents stored
        - you can use SQL to access the data
    - MongoDB
        - usually used for migrating an existing DB
    - Cassandra
        - also usually used for migrating
    - Azure Table
        - different from a table in an Azure storage account
    - Gremlin (Graph)
        - based on nodes, edges/relations
- you can make the CosmosDB account geo-redundant (which means you'll be paying double for storage)
- if you pick geo-redundant storage you can enable the paired region to make writes to the account (doubles the cost of the account again)
- two copies of DB backups are stored for you for free
    - you can then choose between locally- or geo-redundant storage
- once you have an account
    - you can create containers and explore them through the Data Explorer
    - you can create role-based access controls
    - you can add/remove read regions on the replicate page
        - the synchronizing and replication happens automatically
    - on the keys page you can view your primary and secondary access keys, both the read-write and the read keys, as well as the URI for the account
- creating a container
    - you get to pick an RU/second level (400+)
    - 1 RU/s: the amount of compute needed to read 1kb of data in one second
    - the higher the RU, the more the DB will cost you
    - you can choose to share those RU/s across all the containers in your DB
    - partition key: the field by which CosmosDB will physically split up your data
- default consistency (how the data syncs across replicated regions)
    - strong: data is automatically synced each time it changes
    - bounded stateless: you set the maximum amount of time you will allow before data has to be synced
    - session: this is the default, the clients in the current session will see their data synced across whatever regions they're accessing, but for regions that aren't being currently accessed there are undefined delays between syncs
    - consistent prefix: no guarantee of when the data gets synced, but it'll always be in the right order
    - eventual: no guarantee of when the data gets synced and no guarantee of order

### SQL database
- SQL Server resource
    - the simplest way to migrate your existing DBs is to create a
    - not cheapest
    - you'd essentially have a VM running what you used to have hosted on your own machines
    - used if you need to really fine-tune the DBs and/or manage CPU precisely
- Azure SQL Server resource
    - also a simple option if you have basic DBs
    - migrate data and change connection strings, that's it
    - cheaper
    - usually the best option
    - PaaS
    - you pay per DB
    - there are also MariaDB, MySQL and PostgreSQL options
    - elastic pool
        - you can have multiple DBs sharing the same compute resources
        - good if the DBs are independent and they won't both get flooded with traffic at the same time
    - DTU: data transaction unit, a combo of CPU and memory resources
        - you are charged per DTU
        - the charge per DTU is different depending on the pricing tier you choose
        - performance models: Basic, Standard, Premium
    - there is now also a vCore model that is used instead of the DTU model
        - you get to pick
            - General Purpose, Hyperscale and Business Critical pricing tiers
            - provisioned / serverless
                - serverless scales up or down automatically
                - you can't predict your cost in advance
            - how many cores you want
            - how much memory you want
        - much more expensive than the DTU model
    - when you create a DB you're also creating a server (unless you specified an existing server to put the DB on)
    - you can set up Active Directory access
    - you add IPs to the firewall rules of the server to access the DB/s
    - geo replication
        - you can replicate your data in multiple regions
        - each time, you create a new server
        - read-only
        - you pay double what you did if you only have the DB on your primary server
- Azure SQL Managed Instance
    - Azure manages performance and scaling for you
- SQL Data Warehouse
    - used for tons of data
    - used for reporting

### blob containers
- container into which you can put whatever files you want
- access levels
    - private: no anonymous access
    - blob: anonymous read access to blobs only
    - container: anonymous read access to all containers and blobs
- to access a blob/container you still need an access key (I think)
- AzCopy
    - a Windows command line tool
    - you can use it to move files between containers, etc.
    - if you're moving between storage accounts you're going to have different `/SourceKey` and `/DestinationKey` arguments
- leases
    - different clients can "lease" a file while they use it, and that locks out all other users
    - once the client is done with the file, they break the lease so that another client can access it
- access tiers
    - hot: the default, it's cheap to access, expensive to store
    - cool: stored for at least 30 days
    - archive: stored for at least 180 days, cheap to store, expensive to access

### Azure authentication
- Azure Active Directory
    - different than Windows AD
    - you can connect on-prem (Windows AD) with Azure AD
    - if you're connected to Windows AD, you don't have to sync all your Azure AD accounts, i.e. the syncing can go only one way (Windows -> Azure)
    - you can allow users to log in with Google/Facebook/Microsoft


### Azure Access Control


### secure data


### scaling apps and services


### caching and content delivery networks


### monitoring and logging


### consuming Azure services


### application messaging


