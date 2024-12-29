# Azureproject-lab-3
Manage Azure resources by using Azure Resource Manager Templates
Task 1: Create an Azure Resource Manager Template
Sign in to the Azure Portal:

Go to Azure Portal and sign in with your Azure account.

Create a Managed Disk:

Search for and Select Disks: In the search bar, type "Disks" and select it.

Create Disk: On the Disks page, click "Create."

Configure Disk: On the Create a managed disk page, use the following settings:

Subscription: Your subscription

Resource Group: az104-rg3 (create new if necessary)

Disk name: az104-disk1

Region: East US

Availability zone: No infrastructure redundancy required

Source type: None

Performance: Standard HDD

Size: 32 GiB

Review and Create: Click "Review + Create" and then "Create."

Export Template: After deployment, go to the resource, click "Automation" and select "Export template."

Download Template: Review the template and parameters files, then download and save them to your local drive.

Extract Template Files:

Extract Files: Use File Explorer to extract the content of the downloaded file. You should have two JSON files (template and parameters).

Task 2: Edit and Redeploy the Template
Deploy a Custom Template:

Search for Custom Template: In the Azure portal, search for and select "Deploy a custom template."

Build Your Own Template: Select "Build your own template in the editor."

Load File: Click "Load file" and upload the template.json file.

Edit Template: Change disks_az104_disk1_name to disk_name in two places and az104-disk1 to az104-disk2 in one place. Save your changes.

Edit Parameters File:

Edit Parameters: Select "Edit parameters," load the parameters.json file, change disks_az104_disk1_name to disk_name in one place, and save your changes.

Complete Deployment Settings:

Settings: Use the following settings:

Subscription: Your subscription

Resource Group: az104-rg3

Region: East US

Disk_name: az104-disk2

Review and Create: Click "Review + Create" and then "Create."

Verify Deployment:

Go to Resource: Verify az104-disk2 was created.

Check Resource Group: Go to the az104-rg3 resource group and ensure both disks are present.

Review Deployments: In the "Settings" section, click "Deployments" and review the content of the Input and Template blades.

Task 3: Configure Cloud Shell and Deploy Template with PowerShell
Open Cloud Shell:

Select Cloud Shell Icon: Click the Cloud Shell icon in the top right of the Azure Portal or go to Azure Cloud Shell.

Select PowerShell: When prompted, select PowerShell.

Mount Storage Account:

Mount Storage: On the Getting Started screen, select "Mount storage account," choose your subscription, and click "Apply."

Create Storage Account: Select "I want to create a storage account" and complete the creation using the following settings:

Resource Group: az104-rg3

Region: Your region

Storage Account: Create a new storage account with a unique name.

File Share: Create a new file share named fs-cloudshell.

Upload Template Files:

Upload Files: Use the Upload/Download files icon to upload the template.json and parameters.json files from your local machine.

Edit Template:

Edit Template: Navigate to the template JSON file using the editor, change the disk name to az104-disk3, and save the changes.

Deploy Template:

PowerShell Command: Use the following command to deploy the template:

powershell
New-AzResourceGroupDeployment -ResourceGroupName az104-rg3 -TemplateFile template.json -TemplateParameterFile parameters.json
Verify Deployment: Ensure the command completes successfully and verify the disk was created using:

powershell
Get-AzDisk
Task 4: Deploy Template with CLI
Switch to Bash:

Select Bash: Continue in Cloud Shell and switch to Bash.

Verify Files:

List Files: Use the ls command to verify the template files are available.

Edit Template:

Edit Template: Navigate to the template JSON file, change the disk name to az104-disk4, and save the changes.

Deploy Template:

CLI Command: Use the following command to deploy the template:

sh
az deployment group create --resource-group az104-rg3 --template-file template.json --parameters parameters.json
Verify Deployment: Ensure the command completes successfully and verify the disk was created using:

sh
az disk list --output table
Task 5: Deploy Resource using Azure Bicep
Download and Upload Bicep File:

Locate Bicep File: Download the azuredeploydisk.bicep file.

Upload File: Upload the Bicep file to Cloud Shell.

Edit Bicep Template:

Edit Template: Change the managed disk name to Disk4, SKU name to StandardSSD_LRS, and disk size to 32 GiB. Save the changes.

Deploy Bicep Template:

Deploy Command: Use the following command to deploy the Bicep template:

sh
az deployment group create --resource-group az104-rg3 --template-file azuredeploydisk.bicep
Verify Deployment: Ensure the command completes successfully and verify the disk was created using:

sh
az disk list --output table
Cleanup Resources
If you're using your own subscription, you can delete the lab resources to free up resources and minimize costs:

Delete Resource Group:

Azure Portal: In the Azure portal, select the resource group, click "Delete resource group," enter the resource group name, and confirm the deletion.

Azure PowerShell: Use the following command:

powershell
Remove-AzResourceGroup -Name az104-rg3
Azure CLI: Use the following command:

sh
az group delete --name az104-rg3
