# Day 34: Enabling Internet Connectivity for Virtual Machines

The Nautilus DevOps team has encountered an issue with an Azure VM named `devops-vm`. They are unable to install any packages on this VM due to connectivity issues. The team needs to identify the root cause of the problem and resolve it to restore normal operations.

- Investigate the connectivity issue preventing package installation on the Azure VM `devops-vm`.
- Implement a solution to resolve the connectivity issue and restore package installation capabilities on the VM.

Note: The SSH key required to access the Azure VM is already created and added to the VM's authorized keys. You can find the SSH key at `/root/.ssh/id_rsa` on the `azure-client` host.

## Task 1: identify the connectivity issue

**SSH into the VM from azure-client host:**

```sh
ssh azureuser@<vm-public-ip>
```

**Check internet reachability:**

```sh
ping 8.8.8.8
```
<img width="1140" height="156" alt="image" src="https://github.com/user-attachments/assets/bb6f03cc-7904-46b7-a893-07d70b54e206" />

**Now check outbound rule for the vm**

Go to `Networking` > `Network settings` and check for `Outbound port rules` section.

<img width="997" height="180" alt="image" src="https://github.com/user-attachments/assets/bac38279-b1ac-4389-ad90-9c039cb2e754" />


>[!Note]
> The problem is that **Outbound port rule** has a rule `Block-All-Outbound`


## Task 2: Fix the connectivity issue

1. Go to `devops-vm` network security group and select `Outbound security rules` from navigation pane.

   <img width="239" height="405" alt="image" src="https://github.com/user-attachments/assets/2d36127f-b7a9-4350-afdc-8ac0b0f1788d" />

2. Select `Block-All-Outbound` rule and delete it.

   <img width="1085" height="333" alt="image" src="https://github.com/user-attachments/assets/cf56cf1d-bf60-4ac1-89ac-a2df65e55330" />

3. Review `Outbound security rules` after deletion.

   <img width="1083" height="291" alt="image" src="https://github.com/user-attachments/assets/6ff5631c-d563-481b-a420-a75c194e7274" />

4. Next try to reach internet from vm using ping to see if it works.

   ```sh
   ping 8.8.8.8
   ```
   
   <img width="1069" height="231" alt="image" src="https://github.com/user-attachments/assets/547bbfd4-829d-433d-8f5c-b9f5103f85d3" />

6. Also update packages in the vm.

   ```sh
   sudo apt update
   ```

   <img width="1048" height="111" alt="image" src="https://github.com/user-attachments/assets/e3f3fdda-0411-4cbb-954f-6543dc5918e7" />
