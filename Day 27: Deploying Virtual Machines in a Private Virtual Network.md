# Day 27: Deploying Virtual Machines in a Private Virtual Network


The Nautilus DevOps team is expanding their Azure infrastructure and requires the setup of a private Virtual Network (VNet) along with a subnet. This VNet and subnet configuration will ensure that resources deployed within them remain isolated from external networks and can only communicate within the VNet. Additionally, the team needs to provision a Virtual Machine (VM) under the newly created private VNet. This VM should be accessible over SSH from within the VNet only, allowing for secure communication and resource management within the Azure environment.

The name of the VNet must be `xfusion-priv-vnet`, create a subnet named `xfusion-priv-subnet` under the same. Further, create a **Virtual Machine** named `xfusion-priv-vm` under this VNet. Additionally, create a **Network Security Group (NSG)** named `xfusion-priv-nsg`, and ensure that the NSG rules for the VM allow access only from within the VNet's CIDR block. Ensure all resources are created in the `East US` region.

## Create a virtual network

1. In the portal, search for and select `Virtual networks`.
2. On the **Virtual networks** page, `select + Create`.

   <img width="1128" height="325" alt="image" src="https://github.com/user-attachments/assets/4c5d3707-898e-4f14-93c9-68bd79f9a3c4" />

3. On the `Basics` tab of Create virtual network, enter, or select the following information:

   <img width="1247" height="476" alt="image" src="https://github.com/user-attachments/assets/64379041-87c6-46f7-8f11-cfdd83551ca4" />

4. Select `Next` to proceed to the `IP Addresses` tab.

   <img width="1259" height="497" alt="image" src="https://github.com/user-attachments/assets/c690362c-823b-4fb8-985c-f36cbd4f1733" />

5. Click on `+ Add a subnet` and add `devops-pub-subnet`.

   <img width="585" height="447" alt="image" src="https://github.com/user-attachments/assets/6229a809-1ea2-458b-ba86-8739710dc171" />

5. Also enable the subnet as Private subnet.

   <img width="585" height="280" alt="image" src="https://github.com/user-attachments/assets/c173f13a-53f1-4950-ab6b-d09d0677f5ce" />

7. Verify new subnet added on the subnet list.

   <img width="1251" height="477" alt="image" src="https://github.com/user-attachments/assets/7e053120-5aed-484d-8041-74b179eff910" />

8. Select `Review + create` at the bottom of the window. When validation passes, select `Create`.

## Create a VM named `devops-pub-vm` under this VNet.

- In the portal, search for and select `Virtual machines`.
- In Virtual machines, select `+ Create`, and then select `Azure virtual machine`.
- On the `Basics` tab of `Create a virtual machine`, enter or select the following information:

  <img width="1239" height="322" alt="image" src="https://github.com/user-attachments/assets/d20d24e8-974d-47fe-ab9f-0c3d98bd90e5" />

  `For the VM, select size Standard_B1s and OS disk type Standard HDD`
- Select the `Networking` tab. Enter or select the following information:

  <img width="1256" height="387" alt="image" src="https://github.com/user-attachments/assets/8963aba3-edca-4f50-9f6f-588f5820d7f0" />

- Leave the rest of the settings at the defaults and select `Review + create`.
- Review VM after deployment.

  <img width="1096" height="385" alt="image" src="https://github.com/user-attachments/assets/53eea9d8-a36f-4776-b300-bde0777de4d8" />

