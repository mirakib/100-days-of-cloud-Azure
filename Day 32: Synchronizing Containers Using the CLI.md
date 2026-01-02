# Day 32: Synchronizing Containers Using the CLI

As a member of the Nautilus DevOps Team, your task is to perform the following:

**Create a New Private Azure Blob Container**: Name the container `nautilus-dest-3717` under the storage account `nautilusst19421`.

**Data Migration**: Migrate the file `nautilus.txt` from the existing `nautilus-source-24862` container to the new `nautilus-dest-3717` container.

**Ensure Data Consistency**: Ensure that both containers have the file `nautilus.txt` and confirm the file content is identical in both containers.

**Use Azure CLI**: Use the Azure CLI to perform the creation and data migration tasks.

## Step 1: Create the new private container

```sh
az storage container create \
  --account-name nautilusst19421 \
  --name nautilus-dest-3717 \
  --public-access off
```

>[!Note]
> `--public-access off` ensures the container is `private`.

## Step 2: Copy the file from the source container to the new container

```sh
az storage blob copy start \
  --account-name nautilusst19421 \
  --destination-container nautilus-dest-3717 \
  --destination-blob nautilus.txt \
  --source-account-name nautilusst19421 \
  --source-container nautilus-source-24862 \
  --source-blob nautilus.txt
```

>[!Note]
> This uses server-side copy, so it’s fast and doesn’t download/upload locally.


## Step 3: Verify both containers have the file

**List blobs in source container:**

```sh
az storage blob list \
  --account-name nautilusst19421 \
  --container-name nautilus-source-24862 \
  --output table
```

```sh
# List blobs in destination container
az storage blob list \
  --account-name nautilusst19421 \
  --container-name nautilus-dest-3717 \
  --output table
```

## Step 4: Verify file content is identical

**Download from source:**

```sh
az storage blob download \
  --account-name nautilusst19421 \
  --container-name nautilus-source-24862 \
  --name nautilus.txt \
  --file ./source-nautilus.txt
```

**Download from destination:**

```sh
az storage blob download \
  --account-name nautilusst19421 \
  --container-name nautilus-dest-3717 \
  --name nautilus.txt \
  --file ./dest-nautilus.txt
```
