# Day 5: Create a Virtual Network (IPv4) in Azure

Create a **`Virtual Network`** (VNet) named **`nautilus-vnet`** in the **`East US`** region with **`192.168.0.0/24`** IPv4 CIDR.

The following procedure creates a virtual network with a resource subnet, an Azure Bastion subnet, and a Bastion host:

- In the portal, search for and select **`Virtual networks`**.
- On the **`Virtual networks`** page, select + **`Create`**.
- On the **`Basics`** tab of **`Create virtual network`**, enter, or select the following information:

  <img width="1193" height="475" alt="image" src="https://github.com/user-attachments/assets/550d241f-212b-47bc-882f-ead5f9b3d91a" />

- Select **`Next`** to proceed to the **`Security`** tab.
- In the **`Azure Bastion`** section, select **`Enable Azure Bastion`**.

  <img width="1216" height="483" alt="image" src="https://github.com/user-attachments/assets/ae417028-abc4-4b54-a33d-45c1dca77be0" />

- Select **`Next`** to proceed to the **`IP Addresses`** tab.
- In the address space box in **`Subnets`**, select the **`default`** subnet.

  <img width="1194" height="483" alt="image" src="https://github.com/user-attachments/assets/4ce67e19-fba8-4e9e-a859-7b2b74c4daf3" />

- In **`Edit subnet`**, enter or select the following information: `Choose` **`10.0.0.0/24`** `Address Space for challenge requirment`

  <img width="1366" height="568" alt="image" src="https://github.com/user-attachments/assets/ecb068f9-9326-4771-9e39-b101db9864dd" />

- Select **`Save`**.
- Select **`Review + create`** at the bottom of the window. When validation passes, select **`Create`**.

  <img width="420" height="60" alt="image" src="https://github.com/user-attachments/assets/3c7f47e2-aa98-42b2-8669-b11165aa721a" />

- Verify Deployment

  <img width="776" height="302" alt="image" src="https://github.com/user-attachments/assets/3366d675-dd2f-4598-93b8-6f48992ef35b" />


**Azure Docs to be followed: [Create an Azure Virtual Network](https://learn.microsoft.com/en-us/azure/virtual-network/quickstart-create-virtual-network?tabs=portal)**
