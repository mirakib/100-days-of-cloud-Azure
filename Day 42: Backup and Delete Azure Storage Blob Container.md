# Day 42: Backup and Delete Azure Storage Blob Container

The Nautilus DevOps team is currently engaged in a cleanup process, focusing on removing unnecessary data and services from their Azure environment. As part of the migration process, several resources were created for one-time use only, necessitating a cleanup effort to optimize their Azure environment.

A private blob container named `devops-blob-30549` already exists in the `East US` region under storage account `devopsst20886`.

1) Copy the contents of `devops-blob-30549` blob container to the `/opt` directory on the `azure-client` host (the landing host once you load this lab).

2) Delete the blob container `devops-blob-30549` from the storage account.


## Task 1: Locate container and get access key

1. **Go to `Storage center` from azure portal and locate storage account `devopsst20886`.**

   <img width="1365" height="456" alt="image" src="https://github.com/user-attachments/assets/09376d37-76f2-43bf-a966-724430e81f41" />

2. **Click on the storage account and select `Access key` from its menu.**

   <img width="827" height="447" alt="image" src="https://github.com/user-attachments/assets/13290ccb-aeaf-4868-a5db-ebd85453ce24" />

## Task 2: Copy contents from container to host

1. **Login to azure from azure-client host.**

   ```sh
   az login
   ```

2. **Copy blob container contents to azure-client host `/opt`.**

   ```sh
   az storage blob download-batch \
    --account-name devopsst20886 \
    --account-key "<AZURE_STORAGE_KEY>" \
    --source devops-blob-30549 \
    --destination /opt
   ```

   **Expected:**

   ```
   Finished[#############################################################]  100.0000%
    [
      "devops.txt"
    ]
   ```

3. **Delete the blob container**

   ```sh
   az storage container delete \
    --account-name devopsst20886 \
    --account-key "<AZURE_STORAGE_KEY>" \
    --name devops-blob-30549
   ```

   **Expected:**

   ```
   {
    "deleted": true
   }
   ```

