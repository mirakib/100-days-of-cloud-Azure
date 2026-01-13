# Day 43: Configuring Azure VM with Application Gateway

The Nautilus Development Team needs to set up a new Azure Virtual Machine (VM) and configure it to run a web server. This VM should be part of an Azure Application Gateway (AGW) setup to ensure high availability and better traffic management. The task involves creating a VM, setting up an AGW, configuring a backend pool, and ensuring the web server is accessible via the AGW public IP.

**Create a Network Security Group (NSG)**: Create an NSG named `devops-nsg` and add an inbound security rule `Allow-HTTP` to allow `TCP` traffic on port `80`.

**Create a Virtual Machine**: Create a VM named `devops-vm` using any available `Ubuntu` image. Configure the instance with the following settings:

- **Size**: Choose a lightweight VM size (e.g., `Standard_B1s`).

- **Authentication**: Use SSH public key authentication. (Please select use existing public key option, create `public-key` locally and paste contents of `~/.ssh/id_rsa.pub`)
- **OS Disk**: Use a `Standard HDD`.

- **Networking**: Under the Advanced section, attach an existing NSG (e.g., `devops-nsg`).

Additionally, configure the instance to run a user data script during launch that:

- **Install** the Nginx package.

- **Start** the Nginx service.

**Set up an Application Gateway**: Set up an Azure Application Gateway named `devops-agw` with the following:

- Create and Associate it with a public IP address named `devops-agw-ip`.

- Attach the `backend pool:devops-backendpool` to the VM `devops-vm`.
  
- Select a subnet for the Application Gateway (you can create a new one if needed).

**Configure HTTP Settings**: Create an HTTP setting named `devops-http-settings` on port `80`

**Route Traffic**: Add a listener named `devops-listener` and a routing rule named `devops-routing-rule` to route traffic from the AGW frontend to the backend pool:

- **Listener**: Frontend IP = public IP, Frontend port = 80, Protocol = HTTP

- **Routing rule**: Connects devops-listener to `devops-backendpool` using `devops-http-settings`.

**NSG Adjustments**: Make sure the NSG attached to the VM **allows inbound** TCP traffic on port `80`, so the Nginx server running on `devops-vm` is accessible via the Application Gateway public IP.

>[!Note]
> Wait for the Application Gateway resource to be fully deployed before proceeding with the next steps. Deployment may take several minutes to complete.


## Task 1: Create network security group

1. `Go to Azure Portal` > `Create a resource` > `Networking` > `Network Security Group`.

   <img width="1365" height="579" alt="image" src="https://github.com/user-attachments/assets/a88c068a-182e-45c6-ac2c-fc1c1155ba88" />

2. Enter name `devops-nsg` and choose region `East US`.

   <img width="1365" height="429" alt="image" src="https://github.com/user-attachments/assets/8da5d9bc-5b89-40c0-892f-420ec7ebc925" />

3. Click `Review + create` > `Create`.

   <img width="1365" height="452" alt="image" src="https://github.com/user-attachments/assets/15201662-2335-4371-a10d-b3d505218c27" />

4. After creation, go to the `Network Security Groups` → `Inbound security rules` → `+ Add`.

   <img width="1365" height="403" alt="image" src="https://github.com/user-attachments/assets/acee7d81-0311-4250-a87b-f53c75177642" />

5. Add an inbound security rule `Allow-HTTP` to allow `TCP` traffic on port `80`.

   <img width="523" height="579" alt="image" src="https://github.com/user-attachments/assets/ac5a70f7-db24-4019-af62-29a27913ed2a" />

6. Preview NSG is ready with HTTP allowed.

   <img width="1128" height="291" alt="image" src="https://github.com/user-attachments/assets/3b7cba56-09a3-469c-87dc-2a84def67747" />


## Task 2: Create a Virtual Machine

1. Go to Virtual machine dashboard and click `Create`.

   <img width="1128" height="448" alt="image" src="https://github.com/user-attachments/assets/53e30044-c79c-4b3d-902a-f01fa346dc8d" />

2. Create a VM named `devops-vm` using any available `Ubuntu` image.

   <img width="1365" height="355" alt="image" src="https://github.com/user-attachments/assets/4d625647-5430-43aa-be6f-f079e4083445" />

3. In the `Size` section, choose a lightweight VM size (e.g., `Standard_B1s`).

   <img width="1365" height="270" alt="image" src="https://github.com/user-attachments/assets/0fb22179-e129-43d6-9de5-7492ce8266cf" />

4. Select `Use existing public key`, then paste contents of `~/.ssh/id_rsa.pub` from azure-client host.

   Create SSH keys with `ssh-keygen -t rsa` in azure-client host fist.

   <img width="1365" height="367" alt="image" src="https://github.com/user-attachments/assets/d3df8c7c-74c5-4080-b49c-86471d2c4647" />

5. CLick `Next` and go to `Disk` tab and select `OS disk type` as `Standard HDD`.

   <img width="1365" height="284" alt="image" src="https://github.com/user-attachments/assets/886cc5b6-7f59-4d42-b101-260087f1be11" />

6. Proceed to `Advanced` tab and paste Nginx install and start script under `Custom data`.

   ```sh
   #!/bin/bash
   sudo apt update
   sudo apt install -y nginx
   sudo systemctl enable nginx
   sudo systemctl start nginx
   ```

   <img width="1365" height="259" alt="image" src="https://github.com/user-attachments/assets/5ed9708c-2f13-4c15-ab74-e81af6d92ab0" />

7. Go to `Review + create` and click `Create`.

   <img width="1365" height="554" alt="image" src="https://github.com/user-attachments/assets/803402ad-9e37-458f-9c33-db316d8c1b5a" />


## Task 3: Create Application Gateway

1. Go to `Application gateway` dashboard and choose `Application gateway` in `Create`.

   <img width="1365" height="546" alt="image" src="https://github.com/user-attachments/assets/2b421d73-f02e-452a-845c-42df2157a972" />

2. Set up an Azure Application Gateway named `devops-agw` and `Tier` to `Basic`.

   <img width="1365" height="269" alt="image" src="https://github.com/user-attachments/assets/1341a104-507f-4816-8023-d984272727d3" />

3. Add instance count as you wish. Preferred 1 for minimum and 2 for maximum.

   <img width="1365" height="240" alt="image" src="https://github.com/user-attachments/assets/aa38f4a4-4742-47ed-81fa-592d3ce05ca2" />

4. Create a separate new subnet by clicking `+ Subnet`.

   <img width="1128" height="198" alt="image" src="https://github.com/user-attachments/assets/3ae55b00-da6e-4c79-a1c0-29727312ee0e" />

5. Enter subnet details with new any relavant name.

   <img width="764" height="571" alt="image" src="https://github.com/user-attachments/assets/a9b6c43c-f002-4be8-9299-ef75985893d5" />

6. Verify newly created subnet.

   <img width="1128" height="259" alt="image" src="https://github.com/user-attachments/assets/b591ee11-4685-429d-8d3d-8751e825f967" />

7. Select the new subnet under subnet you just created.

   <img width="1365" height="171" alt="image" src="https://github.com/user-attachments/assets/116cf10e-b59b-42ca-85cf-7ce3a99fd557" />

8. On `Frontends` tab, selct `Add new` then enter name as `devops-agw-ip`.

   <img width="1365" height="497" alt="image" src="https://github.com/user-attachments/assets/bfa0056f-44ac-4e5e-81c9-3011285ed464" />

9. On `Backends` tab, enter following:
    - **Backend Name**: `devops-backendpool`
    - **Add target**:
      - **Target type**: Virtual machine and select the private IP of `devops-vm`.

    <img width="1365" height="579" alt="image" src="https://github.com/user-attachments/assets/4b23b8a0-077a-4f53-b7b7-dd7f1426f87a" />

11. Next go to `Configuration` tab and add routing rule.

    <img width="1365" height="438" alt="image" src="https://github.com/user-attachments/assets/47e08d07-19f5-41ff-b41b-ff84596aed74" />

12. Add a listener named `devops-listener` and a routing rule named `devops-routing-rule` to route traffic from the AGW frontend to the backend pool:

    <img width="764" height="577" alt="image" src="https://github.com/user-attachments/assets/6e7270ad-5fbf-4695-84d1-c8969a985cbc" />

13. Next in the `Add a routing rule` dialouge box's `Backend targets` tab, select `Backend target` as `devops-backendpool`.

    <img width="764" height="574" alt="image" src="https://github.com/user-attachments/assets/3f25daac-0a12-4b2e-9bc8-eed6825b02e1" />

14. In the `Add a routing rule` dialouge box's `Backend targets` tab, click `Add new` for `Backend settings` option and enter name `devops-http-setting` and leave rest as default.

    <img width="764" height="579" alt="image" src="https://github.com/user-attachments/assets/1517d536-6d19-4607-bf4a-a5e0e29c61e5" />

15. Preview Configuration tab

    <img width="1365" height="438" alt="image" src="https://github.com/user-attachments/assets/6f9dc85d-d080-487c-8a12-cc623472b8e6" />

    Routing Rule links everything: `Frontend IP / Listener → HTTP settings → Backend pool (VM)`
    
16. Go to `Review + create` tab and click `Create`.

>[!Note]
> **Deployment can take 5–10 minutes.**


## Task 4: Attach NSG to Vm

1. Go to `Virtual Networks` → `devops-vnet` → Subnets (`default`)

3. Under `Network security group`, attach `devops-nsg` → `Save`

## Task 5: Verify HTTP Access

1. Ensure Nginx is running on `devops-vm`.

   ```sh
   sudo systemctl status nginx
   ```

   <img width="1206" height="211" alt="image" src="https://github.com/user-attachments/assets/d48c5daf-773b-434c-989b-4de419eafcb6" />

2. Access `devops-agw`'s frontend public ip from web and you should see nginx welcome page.

   <img width="1366" height="225" alt="image" src="https://github.com/user-attachments/assets/1bd67871-17b8-4684-986a-934e3c4b0468" />
