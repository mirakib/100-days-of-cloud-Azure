# Day 24: Securing Virtual Machine SSH Access

The Nautilus DevOps team needs to set up a new Virtual Machine (VM) on the Azure cloud that can be accessed securely from their landing host (azure-client). Follow the steps below to complete this task:

- **Create an SSH Key**: On the `azure-client` host, check if an SSH key already exists. If it doesn’t exist, create a new SSH key on the `azure-client` host that will be used for password-less SSH access.
- **Create a Virtual Machine**: Use the Azure Portal or Azure CLI to create a new Virtual Machine named `devops-vm` in the `westus` region. Set the VM size to `Standard_B1s` and configure the VM with SSH access for the `azureuser` account using the newly created SSH key.
- **Configure SSH Access**: Ensure that the SSH key from the azure-client host is added to the azureuser account on `devops-vm`, enabling secure, password-less SSH access from the `azure-client` host.
- **Verify Connectivity**: Test the connection from `azure-client` to `devops-vm` using SSH to confirm that password-less access has been set up correctly.

## Create an SSH Key on the `azure-client` host, check if an `SSH` key already exists.
   - Check existing SSH keys:
     ```bash
     cd .ssh
     ls -a
     ```
   - Create SSH key:

     ```bash
     ssh-keygen -t rsa
     ```

## Create a Virtual Machine

   - Create a new Virtual Machine named `devops-vm` in the `westus` region.

     <img width="695" height="110" alt="image" src="https://github.com/user-attachments/assets/58aeb1ba-eaf8-434e-a41c-796536530aeb" />

   - Set the VM size to `Standard_B1s`

     <img width="684" height="190" alt="image" src="https://github.com/user-attachments/assets/f23d4b06-318f-4380-95ce-2b7c31227196" />

   - Configure the VM with SSH access for the `azureuser` account using the newly created SSH key.

     <img width="717" height="208" alt="image" src="https://github.com/user-attachments/assets/0011ed0b-cba1-41a5-93a6-7c21efb84d3c" />

## Configure passwordless SSH Access

1. Ensure that the SSH key from the `azure-client` host is added to the azureuser account on `devops-vm`.
   - Copy `id_rsa.pub` from `azure client` to `devops-vm` `authorized_keys` of user `azure-user`.
2. Enable secure, password-less SSH access from the `azure-client` host.

   ```bash
   ssh azureuser@<devops-vm-public-key>
   ```
   

     
