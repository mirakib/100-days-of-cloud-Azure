# Day 6: Create a Subnet in Azure Virtual Network

For this task, create a Virtual Network (VNet) named `datacenter-vnet` and one subnet named `datacenter-subnet` within the VNet in the `East US` region. Make sure the IPv4 address range is `10.0.0.0/16`.

Steps:

1. Under the **Basic** tab, create **`Virtual network`** with existing **resource group** with name **`datacenter-vnet`** in **`EAST US`** region.

   <img width="1248" height="471" alt="image" src="https://github.com/user-attachments/assets/3f138330-83f4-4608-a72f-5c916659b7cf" />

2. Click **Next**, Go to **IP Address** tab and edit the default subnet with name **`datacenter-subnet`** and **Save**

   <img width="585" height="574" alt="image" src="https://github.com/user-attachments/assets/6ece7c3a-3c93-448f-ae4f-624a22813b97" />

3. After renaming the default subnet, verify subnet name and required address space. in this case, it is **`10.0.0.0/16`**

   <img width="1242" height="483" alt="image" src="https://github.com/user-attachments/assets/fe33c6b2-6d68-4125-bdff-1a940928d915" />

4. Select **Review + Create**, **Create**.

   <img width="1238" height="483" alt="image" src="https://github.com/user-attachments/assets/e718d069-4f39-4255-b05e-9fb106f46b28" />

5. Verify deployment.

   <img width="763" height="391" alt="image" src="https://github.com/user-attachments/assets/3af17197-d583-4178-a9e4-d336c0641f2a" />
