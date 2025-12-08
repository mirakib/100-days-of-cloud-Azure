# Day 9: Attach Network Interface Card (NIC) to Azure Virtual Machine

- An existing VM named **`nautilus-vm`** and a network interface named **`nautilus-nic`** already exist in the **`West US`** region.
- Attach the network interface **`nautilus-nic`** to the VM **`nautilus-vm`**.
- Ensure the NIC's status is **`attached`** before submitting the task.
- Make sure that the virtual machine initialization has been completed before submitting this task.

Azure Docs to be followed: [Add a network interface to an existing VM](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-network-interface-vm#add-a-network-interface-to-an-existing-vm)

## To add a network interface to your virtual machine:

1. Go to the [Azure portal](https://portal.azure.com/) to find an existing virtual machine. Search for and select `Virtual machines`.
2. Select the name of your VM. The VM must support the number of network interfaces you want to add. To find out how many network interfaces each VM size supports, see the sizes in Azure for [Sizes for virtual machines in Azure](https://learn.microsoft.com/en-us/azure/virtual-machines/sizes).
3. In the VM `Overview` page, select `Stop`, and then `Yes`. Then wait until the `Status` of the VM changes to `Stopped (deallocated)`.

   <img width="1162" height="312" alt="stop-virtual-machine" src="https://github.com/user-attachments/assets/3439ba64-ef52-4de7-a455-14ff42595061" />

5. Select `Networking > Attach network interface`. Then in `Attach existing network interface`, select the network interface you'd like to attach, and select `OK`.

   <img width="1111" height="422" alt="attach-network-interface" src="https://github.com/user-attachments/assets/ca602741-3700-4a5f-b8ee-c3769a153938" />

7. Select `Overview` > `Start` to start the virtual machine.
