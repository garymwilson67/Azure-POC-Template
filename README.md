# Azure-POC-Template

This repository contains a simple Azure template and configuration instructions which can be used to prepare an Azure account to install and demo a CloudShell Azure deployment. The deployment architecture is intended for demo/POC purposes and is not suitable for production environments.

To prepare an Azure environment for a CloudShell demo, first deploy the basic template by clicking the button below, then follow the instructions in this file to configure the required permissions for the CloudShell application.

## Deployment Architecture

Click the button below to deploy this template to your Azure account:

[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FQualiSystems%2FAzure-POC-Template%2Fmaster%2Fmain_template.json)

The following diagram describes the deployment topology.  

![Deployment Architecture](https://github.com/QualiSystems/Azure-POC-Template/raw/master/POC_CloudShell_AZURE_ARCH.png)

As seen in the above diagram this template will create the following elements in Azure:

1. CloudShell Management VNET
2. CloudShell Management Subnet
3. CloudShell Management Storage
4. CloudShell Management Resource Group
4. CloudShell Management Security Group
5. Windows VM (default DS4_v2) for the following products (installed separately): CloudShell Portal, Quali server (including Execution Server and CloudShell DB)
6. Linux VM (default DS2_v2) for the following product: QualiX
5. CloudShell Sandboxes VNET
6. Peering between the CloudShell Sandboxes VNET and the CloudShell Management VNET

Note that additional VMs may be dynamically allocated for each sandbox.

## Configure Azure API to work with CloudShell

CloudShell Apps communicate with Azure using the Azure API. However, to enable the two platforms to work with each other, you need to add a web application that has permissions to use the Azure API.

During the Azure configuration process you'll obtain an **application ID** and a **secret** key which, along with your subscription ID and tenant ID you'll need to configure CloudShelll. Please pay attention in the steps below to the instructions regarding these important values. 

Follow the instructions below to grant CloudShell access to your Azure cloud account.

1. Login to Azure Portal with your Administrator permissions.

2. Open Azure's **Cloud Shell** by clicking on the header button on the top right corner <br/>
![Azure Portal Cloud Shell Launch Icon](https://docs.microsoft.com/en-us/azure/cloud-shell/media/overview/portal-launch-icon.png) <br/>
If it's your first time using this feature, follow Azure's instructions to create a storage account.

3. Make sure that the shell is opened in Bash mode.

4. Copy the following shell commands, and paste into Azure's shell and press Enter.  
*This script will add an Azure AD application, delegate Azure API permissions to the application and configure the web application as Contributor.*
```
curl https://raw.githubusercontent.com/QualiSystems/Azure-POC-Template/master/api_setup.sh > cloudshell.sh && 
chmod +x cloudshell.sh && 
./cloudshell.sh
```

5. The script should start running, this may take a couple of minutes, please wait until it completes.

6. Copy and store the **Applicate ID**, **Application Secret**, **Tenant ID** and **Subscription ID** somewhere you'll remember and continue to the next step.


### CloudShell Installation

Please contact a Quali representative to continue the installation process.

