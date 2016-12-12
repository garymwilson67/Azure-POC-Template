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
5. Windows VM (default A-3)for the following products (installed separately): CloudShell Portal, Quali server, Execution Server, CloudShell DB
6. Linux VM (default A-2) for the following product: QualiX
5. CloudShell Sandboxes VNET
6. Peering between the CloudShell Sandboxes VNET and the CloudShell Management VNET

Note that additional VMs may be dynamically allocated for each sandbox.

## Configure Azure API to work with CloudShell

CloudShell Apps communicate with Azure using the Azure API. However, to enable the two platforms to work with each other, you need to add a web application that has permissions to use the Azure API.

This configuration is a three-step process:

1. Add an Azure web application
2. Delegate Azure API permissions to the web application
3. Configure the web application as Contributor

During the Azure configuration process below you'll obtain a **tenant** and a **secret** key which, along with your subscription ID and client ID you'll need to configure CloudShelll. Please pay attention in the steps below to the instructions regarding these important values. 

### Add an Azure web application

To add an Azure web application:

![Azure Subscriptions](https://github.com/QualiSystems/Azure-POC-Template/raw/master/images/azure_subscriptions.png)

1. Log in to https://portal.azure.com.
2. From the left pane, select Subscriptions and make sure you have an active subscription.
3. Make sure your subscription has the appropriate permissions.
    1. From the user menu, click My permissions.
    2. In the My permissions blade, click Resource Provider Status.
    3. In the Resource Provider Status blade, click the Status column name twice to show the registered permissions at the top and make sure the following permissions are registered:
        * Microsoft.Compute
        * Microsoft.Support
        * Microsoft.Resources
        * Microsoft.Features
        * Microsoft.Network
        * Microsoft.Authorization
        * Microsoft.Storage
        * Microsoft.ADHybridHealthService
        * Microsoft.OperationalInsights
4. [**Save for later use**] Return to the Subscriptions blade, and copy and store the Subscription ID somewhere you'll remember.
5. Access the Azure Classic Portal at https://manage.windowsazure.com/.
6. From the left pane, select Active Directory and then click the directory containing your subscription.
7. In the directory's page, click the Applications menu and then click the Add button at the bottom.
8. In the window that is displayed, click Add an application my organization is developing.
9. Enter a Name and make sure Web Application and/or Web API is selected. Click Next.
10. In the App properties screen, enter a URL in both fields. For example, "http://quali.com". This is required for creating the web application but does not affect it.
11. Click Complete. The new web application is added.
12. Refresh the page to see the web application.
13. Proceed to the next section to delegate Azure API permissions to the web application.

### Delegate Azure API permissions to the web application

In this section we'll delegate Azure API permissions to the web application we've created. Make sure you save the values mentioned in the steps marked [**Save for later use**] you may not get a chance to retrieve those values again at a later time.

1. Return to the Azure Classic Portal at https://manage.windowsazure.com/.
2. In the directory containing your subscription, click the web application and then click the Configure menu. The Configure page is displayed.

![App Configured](https://raw.githubusercontent.com/QualiSystems/Azure-POC-Template/master/images/app_configured.png)

3. [**Save for later use**] From the properties area, copy and store the Client Id somewhere you'll remember.
4. In the keys area, add a new secret key (for 2 years).
5. Click Save at the bottom of the page. The key is displayed in the keys area.
![Keys Area](https://raw.githubusercontent.com/QualiSystems/Azure-POC-Template/master/images/keys.png)
6. [**Save for later use**] Copy and store the secret key somewhere you'll remember. The CloudShell App will need it for authentication with Azure. Note: The key is displayed only once and will disappear when you leave this page.
7. [**Save for later use**] You will also need the tenant. In the black banner at the bottom of the page, click View Endpoints and copy the tenant from the OAuth 2.0 Authorization Endpoint field (as indicated in the image below) and store it somewhere you'll remember.
![Authorization](https://raw.githubusercontent.com/QualiSystems/Azure-POC-Template/master/images/oauth-authorization.png)
8. In the permissions to other applications area, grant delegated permissions to your web application to allow it to access other Azure resources.
    1. Click Add application.
![Add Application](https://raw.githubusercontent.com/QualiSystems/Azure-POC-Template/master/images/add_application.png)
    2. In the window that is displayed, click Windows Azure Service Management API.
    3. Click Complete.
    4. In the Windows Azure Service Management API row, click the Delegated Permissions dropdown list and make sure the Access Azure Service Management as organization users (preview) check box is selected.

![App Permissions ](https://raw.githubusercontent.com/QualiSystems/Azure-POC-Template/master/images/app_permissions.png)

    5. Click Save at the bottom of the page.

Proceed to the next section to configure the web application as Contributor.

### Configure the web application as Contributor

To configure the Azure web application as Contributor:

1. Return to https://portal.azure.com/.
2. From the left pane, select Subscriptions.
The Subscriptions blade is displayed.
3. Click the required subscription.
4. In the blade that appears, click Access control (IAM).
The Roles blade is displayed.
Note: If you don't see the Roles blade, clear your browser's cache and refresh the page.
5. Click Add
6. In the Add access blade, click Select a role and select the Contributor role.
7. In the Add users blade, search for the web application you created in Add an Azure web application and select it.

![Add Users ](https://raw.githubusercontent.com/QualiSystems/Azure-POC-Template/master/images/add_users.png)

8. Click Select at the bottom of the blade.
9. Click OK at the bottom of the Add access blade.

### CloudShell Installation

Please contact a Quali representative to continue the installation process.

