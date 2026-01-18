# Day 47: SQL Database Migration and Setup

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to Azure. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. As part of this migration, they are focusing on setting up and managing Azure SQL Databases, implementing backup processes, and ensuring data recovery. Below are the tasks they require you to perform:

**Task 1: Create an Azure SQL Database**

Create a publicly accessible Azure SQL Database instance with the following details:

- **Database Name**: `nautilus-sqldb`.
- **Server Name**: `nautilus-server-22153`.
- **Location**: `West US`
- **Backup Storage Redundancy**: `Locally-redundant backup storage`.
- **Hardware Configuration**: `Basic` (For less demanding workloads).
- **Admin Username**: `nautilus-admin`.
- **Admin Password**: Set an appropriate password.
- **Database Size**: Set to `2 GiB`.
- Keep all other configurations as `default`.

Ensure the database is in the **Ready** state.

**Task 2: Create a Storage Account**

- Create a Storage Account named `nautilusst24216`.
- Configure a Blob Container named `nautilus-container-18422` within this storage account.

**Task 3: Backup the Azure SQL Database**

Take a backup of the Azure SQL Database instance nautilus-sqldb and store it in the Blob Container:

- **Storage Account**: `nautilusst24216`.
- **Blob Container**: `nautilus-container-18422`.
- **Backup File Name**: `nautilus-db-backup`.

Ensure the backup is fully exported to the blob container.

**Task 4: Download the Backup**

- Download the backup file from the Blob Container to the `/opt` directory on the `azure-client` host.
- Ensure the file is accessible and properly named based on its extension.

**Requirements for Completion**

- Ensure the SQL Database is in the **Ready** state.
- Confirm the backup is stored in the specified **Blob Container**.
- Verify the backup file is successfully downloaded to the `/opt` directory on the client host.


## Task 1: Create an Azure SQL Database

1. **Go to Azure SQL hub. In the pane for Azure SQL Database, select Show options.**

   <img width="1013" height="320" alt="image" src="https://github.com/user-attachments/assets/06be58a5-b200-4976-afd6-2dc98dc73878" />

2. **In the Azure SQL Database options window, select Create SQL Database.**

   <img width="1434" height="557" alt="image" src="https://github.com/user-attachments/assets/64401b7d-1c23-4964-9c4e-e54b56ff05a8" />

3. **Enter database name and click `Create new` for `Server` option.**

   <img width="1346" height="233" alt="image" src="https://github.com/user-attachments/assets/74cb29fe-9fb8-4e51-8cb5-7142ff9b0f5a" />

4. **For `Authentication`, select `SQL authentication method` and enter `Admin username` and apppriate password.**

   <img width="1365" height="463" alt="image" src="https://github.com/user-attachments/assets/f50b8f75-62b6-48fa-86d8-5ced6cd9142c" />

5. **Click `Create` and preview server.**

   <img width="1348" height="289" alt="image" src="https://github.com/user-attachments/assets/73e8d9de-c525-487c-afca-b64e0de073e9" />

6. **For `Compute + storage, select `Basic`.**

   <img width="1348" height="273" alt="image" src="https://github.com/user-attachments/assets/c9851ea1-48ca-42dd-879b-0fb79b55485d" />

7. **On the `Backup storage redundancy` part, select `Locally-redundant backup storage`.**

   <img width="1350" height="320" alt="image" src="https://github.com/user-attachments/assets/46a29e85-5b2a-473f-a061-4fd212d7b06d" />

8. **Next on the `Networking` tab, choose Connectivity method: `Public endpoint` and Allow Azure services and resources to access this server: `Yes`.**

   <img width="1346" height="419" alt="image" src="https://github.com/user-attachments/assets/4ba69d5d-ead6-49d2-a4cc-bb84afd7fa71" />

9. **Select `Review + create`.**

    <img width="1345" height="488" alt="image" src="https://github.com/user-attachments/assets/816f81ec-402d-4964-b694-d654b620d33b" />

10. **Wait until Status = Online.**

    <img width="1111" height="236" alt="image" src="https://github.com/user-attachments/assets/22e03d8e-d9a8-4d36-ad75-dc12527d2d1c" />


## Task 2: Create a Storage Account and Container

1. **Go to `Storage center` and click `+ Create`.**

   <img width="1194" height="523" alt="image" src="https://github.com/user-attachments/assets/ee00865d-29ff-4375-94e0-b40760da20b5" />

2. **Create storage account with preffered name and other details.**

   <img width="1348" height="300" alt="image" src="https://github.com/user-attachments/assets/36c8f94a-726f-4600-be8b-64db9aecff00" />

3. **Under `Review + create` tab, preview details and click `Create`.**

4. **Go to resource and in the navigation pane, click on `Storage browser`.**

   <img width="1328" height="462" alt="image" src="https://github.com/user-attachments/assets/34663764-2c56-40b4-aae4-b93f1990a575" />

5. **Select `Blob container` and click on `+ Add container`.**

   <img width="1128" height="286" alt="image" src="https://github.com/user-attachments/assets/9a5f52f2-d447-48d2-9674-c5c9ffc02158" />

6. **Enter blob name and click `Create`.**

   <img width="389" height="574" alt="image" src="https://github.com/user-attachments/assets/1aca4325-d7f7-4519-8b38-f47240ae117f" />

7. **Preview Blob container under Storage account.**

   <img width="1128" height="315" alt="image" src="https://github.com/user-attachments/assets/41516a9e-f5e4-4d8e-a292-95fb6cd94ea8" />


## Task 3: Backup (Export) Azure SQL Database

1. **On the Azure Cloud Shell Login to Azure.**

   ```sh
   az login
   ```

2. **Export SQL Database to Blob Storage.**

   ```sh
   az sql db export \
    --resource-group <RESOURCE_GROUP_NAME> \
    --server nautilus-server-22153 \
    --name nautilus-sqldb \
    --admin-user nautilus-admin \
    --admin-password '<SQL_ADMIN_PASSWORD>' \
    --storage-uri https://nautilusst24216.blob.core.windows.net/nautilus-container-18422/nautilus-db-backup.bacpac \
    --storage-key $(az storage account keys list \
    --resource-group <RESOURCE_GROUP_NAME> \
    --account-name nautilusst24216 \
    --query '[0].value' -o tsv)
   ```

3. **Go to Storage Account → Containers Open nautilus-container-18422**

   <img width="1128" height="337" alt="image" src="https://github.com/user-attachments/assets/775f52a5-1361-45b7-8aae-094057c9e03e" />


## Task 4: Download Backup from container to azure client host.

1. **Download the Backup File**
   
   ```sh
   az storage blob download \
     --account-name nautilusst24216 \
     --container-name nautilus-container-18422 \
     --name nautilus-db-backup.bacpac \
     --file /opt/nautilus-db-backup.bacpac \
     --auth-mode login
   ```

2. **Verify file exits at right location in azure client host.**

   ```sh
   ls -lh /opt/nautilus-db-backup.bacpac
   ```

   **Expected:**
  
   ```
   -rw-r--r-- 1 root root 2.8K Jan 18 09:44 /opt/nautilus-db-backup.bacpac
   ```
