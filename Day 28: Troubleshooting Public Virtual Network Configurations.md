# Day 28: Troubleshooting Public Virtual Network Configurations

The Nautilus DevOps Team deployed an Nginx server on an Azure VM in a public VNet named xfusion-vnet. However, the server is still inaccessible from the internet.

As a DevOps team member, complete the following tasks:

- **Verify VNet Configuration**: Ensure `xfusion-vnet` allows internet access.
- **Attach Public IP**: A public IP named `xfusion-pip` already exists. Attach this public IP to the VM `xfusion-vm` to make it accessible from the internet.
- **Ensure Accessibility**: Confirm the VM `xfusion-vm` is accessible on port `80`.

## Task 1: Ensuring `xfusion-vnet` allows internet access.

1. Go to virtual network dashboard and select `xfusion-vnet`.

   <img width="1128" height="228" alt="image" src="https://github.com/user-attachments/assets/bc4144a1-5ea6-4ef8-a32f-191718c9758c" />

2. Associate security group `xfusion-vmNSG` to the subnet `xfusion-subnet`

   <img width="1365" height="615" alt="image" src="https://github.com/user-attachments/assets/a1179dda-285f-4e6b-a10a-a0a347be933c" />

3. Add `Inbound port rule` for `80` with source as `Any` and service as `HTTP`

   <img width="508" height="572" alt="image" src="https://github.com/user-attachments/assets/bc0e7509-eb70-455c-a501-fa668003d301" />

## Task 2: Attach public IP to the VM

2. From the virtual network navigation pane, select `Public IP Addresses`

   <img width="1365" height="293" alt="image" src="https://github.com/user-attachments/assets/aa0cefe7-f717-4db2-bbb4-11261a7744e2" />

3. Select the `xfusion-pip` and click on `Associate`

   <img width="827" height="395" alt="image" src="https://github.com/user-attachments/assets/d7fb223b-ce73-41ba-8108-ddb3b7c5eb03" />

4. From the `Associate public IP address` tab, select `Resource type` as `Network interface` and select the network interface of the `xfusion-vm` on `xfusion-subnet`.

   <img width="523" height="577" alt="image" src="https://github.com/user-attachments/assets/c0b3ac5d-3d05-43b5-beb4-c8d550d1cb0b" />

5. Verify uour `xfusion-vm` now has the public ip `xfusion-pip`.

   <img width="1115" height="210" alt="image" src="https://github.com/user-attachments/assets/a2a13447-9e22-4d3f-89c9-2f841183144f" />
