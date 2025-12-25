# Day 26: Deploying Virtual Machines in a Public Virtual Network

The Nautilus DevOps Team has received a request from the Networking Team to set up a new public VNet to support a set of public-facing services. This VNet will host various resources that need to be accessible over the internet. As part of this setup, you need to ensure the VNet has public subnets with automatic public IP assignment for resources. Additionally, a new VM will be launched within this VNet to host public applications that require SSH access. This setup will enable the Networking Team to deploy and manage public-facing applications.

Create a public VNet named `devops-pub-vnet`, and a subnet named `devops-pub-subnet` under the same, make sure public IP is being auto-assigned to resources under this subnet. Further, create a VM named `devops-pub-vm` under this VNet. Make sure `SSH` port `22` is open for this instance and accessible over the internet. Use the Azure portal to complete the task and ensure that SSH access is configured correctly.

## Create a virtual network

1. In the portal, search for and select `Virtual networks`.
2. On the **Virtual networks** page, `select + Create`.

   <img width="1128" height="325" alt="image" src="https://github.com/user-attachments/assets/4c5d3707-898e-4f14-93c9-68bd79f9a3c4" />

3. On the `Basics` tab of Create virtual network, enter, or select the following information:

   <img width="1259" height="548" alt="image" src="https://github.com/user-attachments/assets/090da097-7f04-40bf-b0c0-be5f336e9e49" />

4. Select `Next` to proceed to the `IP Addresses` tab.

   <img width="1259" height="497" alt="image" src="https://github.com/user-attachments/assets/c690362c-823b-4fb8-985c-f36cbd4f1733" />

5. Click on `+ Add a subnet` and add `devops-pub-subnet`.

   <img width="509" height="563" alt="image" src="https://github.com/user-attachments/assets/d3512700-0f91-41f1-969e-c47af2d414d4" />

6. Verify new subnet added on the subnet list.

   <img width="653" height="254" alt="image" src="https://github.com/user-attachments/assets/e5705f80-8590-4450-94cf-16e138edf642" />

7. Select `Review + create` at the bottom of the window. When validation passes, select `Create`.


## Create a VM named `devops-pub-vm` under this VNet.

- In the portal, search for and select `Virtual machines`.
- In Virtual machines, `select + Create`, and then select `Azure virtual machine`.
- On the `Basics` tab of `Create a virtual machine`, enter or select the following information:

  <img width="1254" height="409" alt="image" src="https://github.com/user-attachments/assets/bab5fa40-8aa1-4b5e-8ee5-2c69cea2d4fd" />

  `For the VM, select size Standard_B1s and OS disk type Standard HDD`
- Select the `Networking` tab. Enter or select the following information:

  <img width="805" height="501" alt="image" src="https://github.com/user-attachments/assets/3fe10c24-f6af-4bec-b723-43c3b52c11a1" />

- Review VM after deployment.

  <img width="1066" height="334" alt="image" src="https://github.com/user-attachments/assets/70aa0527-be75-4130-9522-e2d2490edd11" />

- Leave the rest of the settings at the defaults and select `Review + create`.
