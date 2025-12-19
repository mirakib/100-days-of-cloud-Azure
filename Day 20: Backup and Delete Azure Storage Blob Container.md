# Day 20: Backup and Delete Azure Storage Blob Container

A private blob container named `xfusion-blob-27304` already exists in the `East US` region under storage account `xfusionst23814`.

1) Copy the contents of `xfusion-blob-27304` blob container to the `/opt directory` on the azure-client host (the landing host once you load this lab).

2) Delete the blob container `xfusion-blob-27304` from the storage account.


### To copy contents from Blob container

1. Copy the contents of the blob container to `/opt`

   ```powershell
   sudo az storage blob download-batch \
      --destination /opt \
      --source xfusion-blob-27304 \
      --account-name xfusionst23814 \
      --auth-mode login
   ```

3. Delete the blob container from the storage account
   
   ```powershell
   az storage container delete \
      --name xfusion-blob-27304 \
      --account-name xfusionst23814 \
      --auth-mode login
   ```

