# [Microsoft Azure - Beginner's Guide + AZ-900 - 2021](https://www.udemy.com/course/microsoft-azure-beginners-guide/)

### Azure Virtual Machines
- resources that get created when you create a VM
    - a virtual network
    - disk to store the OS and additional disks you choose
    - NIC with a private and public IP
    - Network Security Group that acts as a firewall
- stopping/deallocating/costs
    - stopping a VM using the Azure Portal stop button
        - "deallocates" the VM which removes it from the phsyical server
        - and deletes anything in the temporary storage disk
        - puts the VM in "stopped" and "deallocated" states
        - restarting the VM will give it a new public IP address
    - shutting down a VM from the VM OS itself
        - doesn't deallocate the VM
        - puts the VM in "stopped" state
        - doesn't delete temporary data
        - keeps original public IP
    - there is a partial compute charge for VMs in the stopped state and no charge for compute time for VMs in the deallocated state
    - there's a partial charge for the OS disk when a VM is deallocated because the disk is a seperate resource from the VM
