# [Microsoft Azure - Beginner's Guide + AZ-900 - 2021](https://www.udemy.com/course/microsoft-azure-beginners-guide/)

### Azure Virtual Machines
- resources that get created when you create a VM
    - a virtual network
    - disk to store the OS and additional disks you choose
    - NIC with a private and public IP
    - Network Security Group that acts as a firewall
- stopping/deallocating/costs
    - stopping a VM using the Azure Portal stop button
        - "deallocates" the VM which removes it from the physical server
        - and deletes anything in the temporary storage disk
        - puts the VM in "stopped" and "deallocated" states
        - restarting the VM will give it a new public IP address
    - shutting down a VM from the VM OS itself
        - doesn't deallocate the VM
        - puts the VM in "stopped" state
        - doesn't delete temporary data
        - keeps original public IP
    - there is a partial compute charge for VMs in the stopped state and no charge for compute time for VMs in the deallocated state
    - there's a partial charge for the OS disk when a VM is deallocated because the disk is a separate resource from the VM
    - you can alter the public IP resource to be a static address that doesn't change even if the VM has been deallocated/reallocated
- availability set
    - when creating a VM you can choose to make it part of an availability set
    - Azure spreads the VMs that are in the set across different fault domains and update domains
        - fault domain: separate server with its own power source and network link, not dependent on other servers
        - update domain: a set of servers that gets updated at the same time
    - you create an availability set with the number of fault (up to 3) and update (up to 20) domains
    - availability sets are for VMs in the same region
    - once a VM is created you can't assign it to a set
    - an availability set is a resource
    - using sets ups VM SLA to 99.95%
- availability zones
    - an availability zone is a collection of data centers within a region
    - instead of separating VMs only across physical servers, zones let you separate them also across a geographic area
    - using zones ups VM SLA to 99.99%
- there is no extra cost for availability zones or sets, but there is a cost for bandwidth between zones ($0.01/GB)
- dedicated host
    - you are the only customer on the physical host
    - your data is more secure
    - you can control maintenance events
- workload
    - an application or a service (e.g. a web app, a DB server) that you can host on Azure using a service (say, a VM that you install the app/server onto)