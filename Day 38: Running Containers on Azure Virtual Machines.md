# Day 38: Running Containers on Azure Virtual Machines

The Nautilus DevOps team needs to set up an Azure Virtual Machine (VM) to interact with an Azure Blob Storage container for storing and retrieving data. The team must create a private storage account, configure Blob Storage, and test the functionality.
Task:

1) **Azure Virtual Machine Setup**:

    The VM named `xfusion-vm` already exists in the `East US` region.

2) **Create a Private Storage Account and Blob Container**:

    Create a storage account named `xfusionstor3544` in the `East US` region with `Locally-redundant storage (LRS)`.
    Create a private Blob container named `xfusion-container3544`.

3) **Retrieve Storage Account Key**:

    Get the storage account's access key to configure access for the application.

4) **Create a Test File**:

    SSH into the VM and create a file named `testfile.txt` in the `/home/azureuser` directory with content: "this is a test file".

5) **Upload the File to Blob Storage**:

    Upload the testfile.txt file to the Blob container xfusion-container3544 using the Azure CLI command:

    az storage blob upload --account-name xfusionstor3544 --account-key <access-key> --container-name xfusion-container3544 --name testfile.txt --file /home/azureuser/testfile.txt


## Task 1: Create a Private Storage Account and Blob Container

1. Go to `Storage center` and select `Blob storage` from menu.

   <img width="251" height="404" alt="image" src="https://github.com/user-attachments/assets/f7fb9342-3f6d-4ac9-ba57-98288232d007" />

2. Click `Create` to create storage account.

   <img width="1093" height="411" alt="image" src="https://github.com/user-attachments/assets/cb8747e9-9560-4d67-aa6f-521bf81666c4" />

3. Create a storage account named xfusionstor3544 in the East US region with Locally-redundant storage (LRS).

   <img width="1340" height="369" alt="image" src="https://github.com/user-attachments/assets/6fd83852-39c1-47df-ad9c-cd5188e14002" />

4. Go to `Review + create` tab and clcik `Create`.

## Task 2: Create a private Blob container

1. To create a `private` Blob container go to storage center and select the newly created account.

   <img width="1128" height="239" alt="image" src="https://github.com/user-attachments/assets/b7350e12-6ea7-4b0e-a974-0c0365854cb9" />

2. From storage account's menu, select `Storage browser`.

   <img width="214" height="493" alt="image" src="https://github.com/user-attachments/assets/3200cb42-e819-4896-8e73-ce9130d60c36" />

3. From `Storage browser`, select `Blob container` click `+ Add container`.

   <img width="608" height="264" alt="image" src="https://github.com/user-attachments/assets/4520be15-4148-4248-9d08-67ec444c5419" />

4. Enter container name and `Anonymous access level` will remain private for now.

   <img width="389" height="574" alt="image" src="https://github.com/user-attachments/assets/247acd1e-1f54-4a1f-975f-e7e3be5632dd" />

5. Preview newly created container.

   <img width="1128" height="298" alt="image" src="https://github.com/user-attachments/assets/a9616470-0748-4ac5-8702-a4812e822d68" />


## Task 3: Retrieve Storage Account Access Key

1. Open Storage accounts → xfusionstor3544, Go to Security + networking → Access keys:

   <img width="210" height="412" alt="image" src="https://github.com/user-attachments/assets/995940ae-e621-4ca5-9072-78fbebc10320" />

2. Copy: Key1 → Key value

   <img width="1111" height="488" alt="image" src="https://github.com/user-attachments/assets/74ce8c32-b71a-4b26-8c69-44410e10d59a" />

## Task 4: SSH into the VM & Create Test File

1. SSH into `xfusion-vm` from azure-client host.

   ```sh
   ssh azureuser@<xfusion-vm-pub-ip>
   ```

2. Create the file

   ```sh
   echo "this is a test file" > testfile.txt
   ```

## Task 5: Upload File to Azure Blob Storage using CLI

1. Ensure Azure CLI is Installed on VM

   ```sh
   az --version
   ```

2. Upload file to the Blob container

   ```sh
   az storage blob upload \
     --account-name xfusionstor3544 \
     --account-key <access-key> \
     --container-name xfusion-container3544 \
     --name testfile.txt \
     --file /home/azureuser/testfile.txt
   ```

   Expected output:

   ```
   Finished[#############################################################]  100.0000%
   {
    "client_request_id": "524f0173-ec89-11f0-afca-cd2b576fde39",
    "content_md5": "XdOcqxxTwsd801KYP5ZB4Q==",
    "date": "2026-01-08T11:58:18+00:00",
    "encryption_key_sha256": null,
    "encryption_scope": null,
    "etag": "\"0x8DE4EAD36E35C77\"",
    "lastModified": "2026-01-08T11:58:19+00:00",
    "request_id": "21386454-e01e-006d-3c96-80d3c0000000",
    "request_server_encrypted": true,
    "version": "2022-11-02",
    "version_id": null
    }
   ```

3. Also verify file uploaded to container from Azure portal

   <img width="608" height="265" alt="image" src="https://github.com/user-attachments/assets/4072ea2a-81ae-4a8c-814a-2701fccb3b9d" />
