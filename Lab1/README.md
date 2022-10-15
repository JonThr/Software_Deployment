# Lab 1
Tasks for Lab 1:
- Create an ARM template that 
	- Deploys an Azure Storage Account (Free Tier) 
	- Deploys an Azure Web-App (Free Tier) 
- Leverages Parameters
	- Name of the storage account, resource group, location, webapp name
	
## Prerequisite
Azure CLI must be installed.
Enter the git repository through Windows Command Prompt or PowerShell and go into the Lab1 directory. 

## Sign in to Azure
To start working with Azure CLI, sign in with your Azure credentials.
```
az login
```
If you have multiple Azure subscriptions, choose the subscription you want to use. Replace SubscriptionName with your subscription name. You can also use your subscription ID instead of your subscription name.
```
az account set --subscription SubscriptionName
```
## Create resource group
When you deploy a template, you can specify a resource group to contain the resources. Before running the deployment command, create the resource group with the following command in Azure PowerShell. 
```
az group create --name myResourceGroup --location "West Europe"
```
## Deploy template

Use the resource group you have created. Give a name to the deployment so you can easily identify it in the deployment history.  The following Azure PowerShell command can be used to deploy the template.
```
az deployment group create --name mydeployment --resource-group myResourceGroup --template-file azuredeploy.json --parameters azuredeploy.parameters.json
```
## References
https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-windows?tabs=azure-cli<br>
https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/syntax#parameters<br>
https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/template-tutorial-create-first-template<br>
https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/parameter-files<br>

