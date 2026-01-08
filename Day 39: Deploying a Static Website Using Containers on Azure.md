# Day 39: Deploying a Static Website Using Containers on Azure

The Nautilus DevOps team has been tasked with creating an internal information portal for public access. As part of this project, they need to host a static website on Azure using an Azure Storage account. The Storage account must be configured for public access to allow external users to access the static website directly via the Azure Storage URL.

Task Requirements:

- Create an Azure Storage account named `datacenterwebst4584` in an existing resource group.
- Configure the Storage account for static website hosting with `index.html` as the index document.
- Allow public access to the static website so that the website is publicly accessible.
- Upload the `index.html` file from the `/root/` directory of the Azure client host to the Storage account's `$web` container.
- Verify that the website is accessible directly through the Azure Storage static website URL.


## Task 1: Create an Azure Storage account

1. **Go to `Storage center` and select `Blob storage` from it's menu.**

   <img width="237" height="317" alt="image" src="https://github.com/user-attachments/assets/fabac6a5-317f-4309-9e7d-eea3d2c1d572" />

2. **Click on `Create` and enter account name with `LRS` redundency setting.**

   <img width="1350" height="420" alt="image" src="https://github.com/user-attachments/assets/22d259d2-32e7-4547-b630-e6aee8a542cb" />

3. **Next go to `Review + create` and click `Create`**

## Task 2: Configure the Storage account for static website hosting 

1. **To enable static web hosting, from storage account menu, select `Data management` > `Static website`.**

   <img width="220" height="398" alt="image" src="https://github.com/user-attachments/assets/f23b6a54-ae98-4379-86f0-c955a5f760d8" />

2. **Enable static web option and enter index document name as `index.html`.**

   <img width="608" height="375" alt="image" src="https://github.com/user-attachments/assets/028f5799-2d0e-4edb-a4bc-58b44c0a519a" />

3. **Click save and you will see an endpoint available.**

   <img width="608" height="462" alt="image" src="https://github.com/user-attachments/assets/3e043346-2719-4df9-aaa2-e8fe0d1d6aaf" />

4. **A blob storage container named `$web` is created for you within the storage account.**

   <img width="846" height="496" alt="image" src="https://github.com/user-attachments/assets/7397e257-5a42-439d-865c-b066eede5db8" />


## Task 3: Allow Public Access

1. **Go to Storage accounts and click on `datacenterwebst4584`.**

   <img width="1119" height="233" alt="image" src="https://github.com/user-attachments/assets/134478d0-5b83-459b-80c6-c18006590820" />

 2. **From the left menu, select `Settings` → `Configuration`.**

    <img width="220" height="421" alt="image" src="https://github.com/user-attachments/assets/8ce1f28f-52a3-4a23-a0ee-d3acb5ee6f37" />

3. **Set: `Allow Blob anonymous access:` Enabled and click Save.**

   <img width="829" height="531" alt="image" src="https://github.com/user-attachments/assets/3b181bee-d61f-4dc6-806c-248e116ecc56" />


## Task 3: Upload file from `azure-client` host to the container and access web.

1. **Get access key of the storage account from it's menu `Security + networking` > `Access key` and copy `key 1`.**

   <img width="824" height="445" alt="image" src="https://github.com/user-attachments/assets/b1a0ffcd-ab0e-411e-9ae3-ffd7249174a3" />
   
2. **Login to Azure (on azure-client)**

   ```sh
   az login
   ```
   **May promt to web and enter code**
   
3. **Upload File to $web Container**

   ```sh
    az storage blob upload \
      --account-name datacenterwebst4584 \
      --account-key <ACCESS_KEY> \
      --container-name '$web' \
      --name index.html \
      --file /root/index.html
   ```

4. **(Optional) Retrive endpoint for web access using CLI**

   ```sh
   az storage account show \
    --name datacenterwebst4584 \
    --query "primaryEndpoints.web" \
    -o tsv
   ```

   **Open the URL in a browser — the site should load publicly.**

5. **You should see `Welcome to KKE labs!` message under the endpoint.**

   <img width="1087" height="121" alt="image" src="https://github.com/user-attachments/assets/a7fe4430-93e3-4687-8e4f-a3c79e82c694" />


