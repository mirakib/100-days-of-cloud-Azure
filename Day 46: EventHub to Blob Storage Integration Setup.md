# Day 46: EventHub to Blob Storage Integration Setup

The Nautilus DevOps team wants to integrate an Azure Virtual Machine with Azure Event Hubs and Azure Blob Storage for centralized log collection and backup. Follow these steps to complete the task:

    Create Azure Event Hubs Namespace:
        Create an Event Hubs namespace named datacenter-namespace in the East US region.
        Select the Standard pricing tier. Make sure to enable Enable Auto-inflate.

    Create an Event Hub:
        Within the namespace, create an Event Hub named datacenter-hub.

    Set Up Azure Blob Storage for Log Backup:
        Create a Storage Account named datacenterst18882 in the East US region.
        Create a container named datacenter-backup-14024 within the Storage Account.
        Ensure the container is publicly accessible for read operations.

    Verify the Virtual Machine Configuration:
        The client host already has a Python script named send_logs.py located under /root. This script is used to send logs to the Event Hub.
        Create a Virtual Machine named datacenter-vm in the East US region.
        Copy the send_logs.py script from the client host to the /home/azureuser directory of the datacenter-vm.
        Modify the script on the VM to also back up the logs to the datacenter-backup-14024 container in the Azure Blob Storage account.

    Verify Logs:
        Ensure the logs are successfully sent to the Event Hub by checking the Event Hubs metrics in the Azure portal.
        Verify that the logs are backed up to the datacenter-backup-14024 container in the Azure Blob Storage.




## Task 1: Create Azure Event Hubs Namespace:

1. Go to `Event Hubs` and click `Create`.

   <img width="1365" height="502" alt="image" src="https://github.com/user-attachments/assets/96458caa-4bbe-4f6a-9a8a-3e24cb1f39af" />

2. Create an Event Hubs namespace named `datacenter-namespace` in the `East US` region and select the `Standard` pricing tier. Make sure to enable `Enable Auto-inflate`.

   <img width="1346" height="387" alt="image" src="https://github.com/user-attachments/assets/d4cbe9a5-9b95-4ce4-a745-4df8b2073250" />

3. On the `Review + create` tab, click `Create`.

   <img width="1346" height="452" alt="image" src="https://github.com/user-attachments/assets/e0aac2ca-498f-4a06-863d-ce807008d62f" />


## Task 2: Create an Event Hub:

1. Go to `datacenter-namespace` dashboard and click on `+ Event Hub`.

   <img width="1344" height="381" alt="image" src="https://github.com/user-attachments/assets/0220ab02-8218-4abd-887e-95289ae5165f" />

2. Enter name and leave others as default.

   <img width="1365" height="438" alt="image" src="https://github.com/user-attachments/assets/f2281335-1f84-486a-b241-a3feee31b942" />

3. On the `Review + create` tab, click `Create`.

   <img width="1346" height="452" alt="image" src="https://github.com/user-attachments/assets/4ba9c4b3-852e-4aa5-93f7-99724d3d3ad4" />



## Task 3: Create a Storage Account and container

1. Go to `Storage center` and click `+ Create`.

   <img width="1194" height="523" alt="image" src="https://github.com/user-attachments/assets/ee00865d-29ff-4375-94e0-b40760da20b5" />

2. Create storage account with preffered name and other details.

   <img width="1257" height="417" alt="image" src="https://github.com/user-attachments/assets/3a23487b-3b46-4ce2-a591-295b3dfcb3cf" />

4. Under `Review + create` tab, preview details and click `Create`.

   <img width="1365" height="554" alt="image" src="https://github.com/user-attachments/assets/f0eda22b-7573-412d-b171-3a90a14aa245" />

5. Go to resource and in the navigation pane, click on `Storage browser`.

   <img width="1365" height="499" alt="image" src="https://github.com/user-attachments/assets/719aa97d-35f3-45a2-9b0e-7b340b2ce37c" />

6. To create public blob container, you have to enable annonymous access from `Navigation pane, Settings, Configuration` and `Save`.

   <img width="846" height="554" alt="image" src="https://github.com/user-attachments/assets/34c95067-f94c-4e0a-b7b4-9072c6ae3596" />

7. Select `Blob container` and click on `+ Add container`.

   <img width="1092" height="479" alt="image" src="https://github.com/user-attachments/assets/aac4ac8d-146c-43ab-8704-c751981877f7" />

8. Enter blob name and click `Create`

   <img width="848" height="573" alt="image" src="https://github.com/user-attachments/assets/9da4bb24-f61e-448b-90e4-1cc873bb5fa9" />

9. Preview Blob container under Storage account.

   <img width="846" height="319" alt="image" src="https://github.com/user-attachments/assets/b1e49763-9819-4da3-ac3b-d8efe0c997c6" />


## Task 4: Create a Virtual Machine

1. In the Virtual machines page, select Create and then Virtual machine. The Create a virtual machine page opens.
2. In the Basics tab, under Project details, make sure the correct subscription is selected and then choose to Create new resource group. Enter myResourceGroup for the name.*.
3. Under Instance details, enter myVM for the Virtual machine name. Under Availability options, select No infrastructure redundancy required. Under Security type, select Standard. Choose Ubuntu Server 22.04 LTS - Gen2 for your Image. Leave the other defaults. The default size and pricing is only shown as an example. Size availability and pricing are dependent on your region and subscription.

   <img width="1348" height="434" alt="image" src="https://github.com/user-attachments/assets/aedf1f4c-31a9-4e3c-b5d0-6074950a784d" />

4. For SSH public key source, leave the default of Generate new key pair, and then enter myKey for the Key pair name.

   <img width="1346" height="205" alt="image" src="https://github.com/user-attachments/assets/7817f727-7c31-4c7b-96f7-a5c80638ce8c" />

5. On the `Disk` tab, select `OS Disk type` as `Standard_HDD`.

   <img width="1348" height="291" alt="image" src="https://github.com/user-attachments/assets/9e1f78f0-1b57-4639-81d6-e2633ff60236" />

6. On the Create a virtual machine page, review the details about the VM you're about to create. When you're ready, select Create.

   <img width="1346" height="447" alt="image" src="https://github.com/user-attachments/assets/7c25efe3-1891-45b0-a03d-cc9146e77584" />

## Task 5: Virtual Machine Configuration:

1. SSH into VM from azure-client host:

   ```sh
   ssh azureuser@<nautilus-vm-pub-ip>
   ```
   
2. Retrive connection string of the event hub.

   <img width="1365" height="579" alt="image" src="https://github.com/user-attachments/assets/adb809ae-2de6-4ef2-bb34-41fe4c453a6a" />

3. Retrive Blob connection string from storage account.

   <img width="1365" height="575" alt="image" src="https://github.com/user-attachments/assets/5a184677-f163-4f2c-b3c1-25992a2e7798" />

4. Copy script to vm and update the python script with connection string.

   `connection_str = "<your_event_hub_connection_string>"`
   
5. Install required packages:

   ```sh
   sudo apt update
   sudo apt install python3-pip -y
   pip3 install azure-eventhub azure-storage-blob
   ```
   
6. Run the script to send logs

   ```sh
   .send_logs.py
   ```

7. Check Event Hub receving logs

   
