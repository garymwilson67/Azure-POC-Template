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
5. Windows VM (default DS4_v2)for the following products (installed separately): CloudShell Portal, Quali server (including Execution Server and CloudShell DB)
6. Linux VM (default DS2_v2) for the following product: QualiX
5. CloudShell Sandboxes VNET
6. Peering between the CloudShell Sandboxes VNET and the CloudShell Management VNET

Note that additional VMs may be dynamically allocated for each sandbox.

## Configure Azure API to work with CloudShell

CloudShell Apps communicate with Azure using the Azure API. However, to enable the two platforms to work with each other, you need to add a web application that has permissions to use the Azure API.

This configuration is a three-step process:

1. Add an Azure web application
2. Delegate Azure API permissions to the web application
3. Configure the web application as Contributor

During the Azure configuration process you'll obtain a **tenant** and a **secret** key which, along with your subscription ID and client ID you'll need to configure CloudShelll. Please pay attention in the steps below to the instructions regarding these important values. 

Please follow the link below for detailed configuration instructions:

<a href="http://help.quali.com/Online%20Help/8.0.0.7489/DRB/Content/Admn/Azure-Cnfg-API.htm" target="_blank">Configure Azure API to work with CloudShell (CloudShell 8.0 EA Online Help)</a>

### CloudShell Installation

Please contact a Quali representative to continue the installation process.

