#CREATE NETWORK RESOURCES & VIRTUAL MACHINE

##CREATE YOUR NETWORK RESOURCES

###Setup your command line

Use the following command to enable the Azure Resource Manager commands:
    
    *azure config mode arm*


Connect to Your Azure Subscription

    *azure login* => starts the interactive login and authenticates your command line


###Create a Resource Group:

Use the following command to list all possible CLI options for Resource Groups:

    *azure group*


Use the following command to create a new resource group with the following details:

    *azure group create –n “CLITestGroup” –l “West US”*


Use the following command to show the details of your resource group:

    *azure group show -n “CLITestGroup”*


###Create a Virtual Network:

Use the following command to list all possible CLI options for network components in Azure:

    *azure network*


Use the following command to list all possible CLI options for Virtual Networks:

    *azure network vnet*


Use the following command to create a new resource group with the following details:

    *azure network vnet create –g "CLITestGroup" –n “TestVNET” -l "West US"*


View your new virtual network in the list of virtual networks using this command:

    *azure network vnet list*


View the details of your new virtual network using this command:

    *azure network vnet show –g “CLITestGroup” –n “TestVNET”*

###Create a SuBNET:

Use the following command to list all possible CLI options for Subnets:

    *azure network vnet subnet*


Use the following command to create a subnet in your existing Virtual Network with the following options:

    *azure network vnet subnet create -g "CLITestGroup" --vnet-name "TestVNET" -n "TestSubnet" --address-prefix 10.0.0.1/24*


View the details of your new subnet using this command:

    *azure network vnet subnet show -g "CLITestGroup" --vnet-name "TestVNET" -n "TestSubnet"*


Use the following command to list all possible CLI options for Public IP Addresses:

    *azure network public-ip*


Use the following command to create a new public IP address in your resource group with the following options:

    *azure network public-ip create -g "CLITestGroup" -n "TestPIP" -l "West US" –-allocation-method “Dynamic”*


Update the public IP address by giving it a unique domain name label. This name must be globally unique in Azure, only consist of alphabetic characters, and is recommended to be at-least 8 characters:
This label will be used to construct the url for yoru virtual machine. 
If your domain name is **demoexample** then youd domain name will end up being 
**demoexample.westus.cloudapp.azure.com**

    *azure network public-ip set -g "CLITestGroup" -n "TestPIP" --domain-name-label "demoexample"

    Note:  if you label is not unique or otherwise not valid, you will receive a message that your request has failed when you try to set the domain name. Simply try again with another domain name label.


View the details of your new public IP address using this command:

    *azure network public-ip show -g "CLITestGroup" -n "TestPIP"


###Create a Network Interface Card

Use the following command to list all possible CLI options for Network Interface Cards:

    *azure network nic*


Use the following command to create a Network Interface Card in your resource group with the following options:

    *azure network nic create -g "CLITestGroup" -l "West US" -n "TestNIC" --subnet-name "TestSubnet" --subnet-vnet-name "TestVNET" --public-ip-name "TestPIP"*


View the details of your new network interface cards using this command:

    *azure network nic show -g "CLITestGroup" -n "TestNIC"


##CREATE A VIRTUAL MACHINE

###List Windows Server Images

Use the following command to list all possible CLI options for images:

    *azure vm image*


Use the following command to list all image **publishers** that match the following options:

    *azure vm image list-publishers -l "West US"*


Use the following command to list all image **offers** that match the following options:

    *azure vm image list-offers -l "West US" -p "MicrosoftWindowsServer"*


Use the following command to list all image **skus** that match the following options:

    *azure vm image list-skus -l "West US" -p "MicrosoftWindowsServer" -o "WindowsServer"*


Use the following command to list all images that match the following options:

    *azure vm image list -l "West US" -p "MicrosoftWindowsServer" -o "WindowsServer" -k "2012-R2-Datacenter"*

    Note: To get list of VM image offers *azure vm image list -p "MicrosoftWindowsServer" -l "West US"*


###Create A Virtual Machine from Image

Use the following command to list all possible CLI options for Virtual Machine:

    *azure vm*


Use the following command to create a virtual machine with the following options:

    *azure vm create -g "CLITestGroup" -n "TestVM" -l "West US" --nic-name "TestNIC" --os-type "Windows" --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20151214 --admin-username "Attendee" --admin-password "<some-long-password>"*

    Note: It can take anywhere from five to fifteen minutes for your virtual machine to be created and ready for use.


View the details of your new network interface cards using this command:

    *azure vm show -g "CLITestGroup" -n "TestVM"*


###Connect to your Virtual Machine

If you do not have it already installed, Install a Remote Desktop Connection client to your local machine

In the command line interface, use the following command to view details of your public IP address:

    *azure network public-ip show -g "CLITestGroup" -n "TestPIP"*

- Observe and record the value of the FQDN property. This property is the url for the virtual machine.
- Open the Remote Desktop Connection software on your local machine.
- For the remote computer name, use the url recorded in the previous steps.
- Enter username and password. In Windows, you may need to add a leading backslash before typing the username so that it doesn't use your current machine's domain. For example, you would type \Attendee in the User name prompt.
onnect to the virtual machine and validate that it is working correctly.
- Close the Remote Desktop Connection software.
- Return to the command line interface.

##CLEAN UP YOUR ENVIRONMENT

Remove the CLITestGroup resource group using the following command:

    *azure group delete –n “CLITestGroup”*

When prompted, type **y** and then press Enter or Return to confirm the delete action.
Close the command line interface application. You are done!
