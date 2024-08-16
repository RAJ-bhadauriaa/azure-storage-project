# azure-storage-project
This project involves managing files in an Azure Storage Account, setting access permissions, and configuring alerts for file uploads.
## Prerequisites
## Azure Services Used

1. **Azure Storage Account:**
   - Service for storing and managing blobs (files) and other data.

2. **Azure Storage Explorer:**
   - Tool for managing Azure Storage resources from your desktop.

3. **Azure Resource Group:**
   - Logical container for organizing and managing Azure resources.

4. **Azure Log Analytics Workspace:**
   - Service for collecting, analyzing, and visualizing log and performance data from Azure resources.

5. **Azure Monitor:**
   - Platform for monitoring Azure resources and setting up alerts based on metrics and logs.

6. **Azure Diagnostics:**
   - Service for collecting diagnostic data from Azure resources, including storage accounts.

7. **Shared Access Signature (SAS):**
   - Token-based mechanism for granting access to Azure Storage resources with specific permissions.

8. **Azure Blob Storage:**
   - Storage service for unstructured data such as text or binary data, including documents.


# Azure Storage Project

## Overview

This project involves managing files in an Azure Storage Account, setting access permissions, and configuring alerts for file uploads. The project consists of the following tasks:
# As an Administrator -----  u have to -
1. Upload a sample internship letter to a private storage account container.
2. Making the container accessible to a specific user.
3. Setting up an alert to notify an administrator when a new file is uploaded.
# As an User -----  u have to -
== Access the letter, signing it digitally, and uploading it back to the container.

## Admin Tasks

### Step 1: Create a Resource Group for Storage Account![Screenshot 2024-08-16 040054](https://github.com/user-attachments/assets/39f5faf7-2e0f-458f-b242-f8a1bb3fe0a1)


1. **Navigate to Azure Portal:**
   - Go to [Azure Portal](https://portal.azure.com/).

2. **Create Resource Group:**
   - In the left-hand menu, click on "Resource groups."
   - Click on "Create."
   - Enter the required details (Name, Region).
   - Click "Review + create" and then "Create."

### Step 2: Configure the Storage Account![Screenshot 2024-08-16 040125](https://github.com/user-attachments/assets/3dec1635-b7df-4981-81be-aed7280237f5)


1. **Navigate to Storage Accounts:**
   - In the Azure Portal, go to "Storage accounts."
   - Click on "Create."

2. **Configure Storage Account:**
   - Enter details such as Subscription, Resource Group, Storage Account Name, Region, and Performance options.
   - Click "Review + create" and then "Create."

### Step 3: Create a Container in the Storage Account![Screenshot 2024-08-16 040207](https://github.com/user-attachments/assets/32272de1-77f3-4385-b509-c1cee98cb557)


1. **Navigate to Containers:**
   - In the storage account menu, under "Data storage," click on "Containers."

2. **Create a Container:**
   - Click on "Create container."
   - Provide a name for the container and set the "Public access level" to "Private."
   - Click "Create."

### Step 4: Upload the Internship Letter and Other Documents

1. **Upload Files:**
   - Go to the created container.
   - Click on "Upload."
   - Select the internship letter and other documents to upload.
   - Click "Upload."

### Step 5: Make the Access Level Private![Screenshot 2024-08-16 040232](https://github.com/user-attachments/assets/28aabc27-a1f1-4d90-89f4-a88cd8b4c12e)


- Ensure that the container’s access level is set to "Private."

### Step 6: Generate SAS Token for Assigning Blob Role to User

1. **Generate SAS Token:**![Screenshot 2024-08-16 040348](https://github.com/user-attachments/assets/f6006ad8-bfea-44ef-ac1b-882c6d0017cc)

   - In the storage account menu, under "Security + networking," click on "Shared access signature."
   - Configure the SAS token settings (permissions, start and end date).
   - Click "Generate SAS and connection string."
   - Copy the SAS token URL.

### Step 7: Create Log Analytics Workspace![Screenshot 2024-08-16 040419](https://github.com/user-attachments/assets/9f933869-d279-4ed9-a1f5-14a90b281c77)


1. **Navigate to Log Analytics Workspaces:**
   - In the Azure Portal, go to "Log Analytics workspaces."
   - Click on "Create."

2. **Create Workspace:**
   - Provide required details.
   - Click "Review + create" and then "Create."

### Step 8: Sync Log Analytics Workspace with Storage Account![Screenshot 2024-08-16 040450](https://github.com/user-attachments/assets/d68d8e03-8ae1-44e9-8097-6c54abd59818)


1. **Navigate to Diagnostic Settings:**
   - In the storage account, click on "Diagnostic settings" under "Monitoring."

2. **Add Diagnostic Setting:**
   - Click "Add diagnostic setting."
   - Name the setting and select the Log Analytics workspace as the destination.
   - Check the "Blob" service.
   - Click "Save."

### Step 9: Create Alert Rule![Screenshot 2024-08-16 040543](https://github.com/user-attachments/assets/d6f8a6ee-0487-4f40-a6d9-360caa396f53)


1. **Navigate to Alerts:**
   - In the Azure Portal, go to "Monitor" and then "Alerts."

2. **Create Alert Rule:**
   - Click "New alert rule."
   - **Scope:** Select the storage account.
   - **Condition:** Click "Add condition."
     - Choose "Custom log search" to use Log Analytics for querying.
     - Use the following KQL query:
       ```kql
       AzureDiagnostics
       | where ResourceType == "STORAGEACCOUNTS"
       | where OperationName == "PutBlob" or OperationName == "PutBlockList"
       | project TimeGenerated, ResourceGroup, Resource, OperationName
       | order by TimeGenerated desc
       ```
   - **Action Group:** Configure an action group to notify the administrator.![Screenshot 2024-08-16 040601](https://github.com/user-attachments/assets/714fce71-3d42-4f0a-954a-19b247686e3c)

   - Provide alert details and click "Create alert rule."

## User Tasks

### Step 1: Download Azure Storage Explorer

1. **Download Storage Explorer:**
   - Download and install ![Screenshot 2024-08-16 043502](https://github.com/user-attachments/assets/83a29bb6-b219-486f-b383-9258ae4e01d8)


### Step 2: Access and Download the Letter

1. **Open Azure Storage Explorer:**
   - Launch the Azure Storage Explorer application.

2. **Add Account Using SAS URL:**![Screenshot 2024-08-16 040750](https://github.com/user-attachments/assets/d90ef33c-768d-4054-94c3-6a3682b46a0d)

   - Click "Add Account" or "Add a resource."
   - Select "Use a shared access signature (SAS) URI."
   - Paste the SAS URL provided by the admin.
   - Click "Next" and follow the prompts to connect.

3. **Download the Internship Letter:**![Screenshot 2024-08-16 040839](https://github.com/user-attachments/assets/d72bf723-d4ed-4f27-8527-690afacc0909)

   - Navigate to the container.
   - Find and download the internship letter.

### Step 3: Digitally Sign the Letter

1. **Sign the Document:**
   - Open the downloaded letter in a PDF editor or digital signature tool.
   - Apply your digital signature.

### Step 4: Upload the Signed Letter Back

1. **Upload the Signed Letter:**
   - In Azure Storage Explorer, navigate to the container.
   - Click "Upload."
   - Select the signed document and click "Upload."
  
#  when the user upload the internship letter back to Container ,admin will get the alert in his/her email![Screenshot 2024-08-16 044329](https://github.com/user-attachments/assets/4473d033-cd33-4061-9061-b588598ea770)






## Further Reading

For detailed insights and learnings from this project, please refer to the [Insights and Learnings](INSIGHTS_AND_LEARNINGS.md) document.



