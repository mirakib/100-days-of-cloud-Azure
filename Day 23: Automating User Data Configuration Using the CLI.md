# Day 23: Automating User Data Configuration Using the CLI

As a member of the Nautilus DevOps Team, your task is to create a VM using Azure CLI with the following specifications:

**Instance Name**: The VM must be named `xfusion-vm`.

**Image**: Use any available `Ubuntu` image to create this VM.

**Custom Script Extension/User Data**: Configure the VM to run a custom script during its launch. This script should:

- Install the `Nginx` package.
- Start the `Nginx` service.

**Network Security Group (NSG)**: Ensure that the VM allows `HTTP` traffic on port `80` from the internet.

**Instructions:**

- Use Azure CLI commands to set up the VM in the specified configuration.
- Ensure the VM is accessible from the internet on port `80`.
- The Nginx service should be running after setup.

## Check existing resource group

```bash
az group list
```
## Create the Cloud-Init Script
Create `cloud-init.txt`

```bash
vi cloud-init.txt
```

Copy the following:
```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
runcmd:
  - systemctl start nginx
  - systemctl enable nginx
```

## Create Azure VM using CLI command

```bash
az vm create \
  --resource-group kml_rg_main-06c66b102d8744e8 \
  --name xfusion-vm \
  --image Ubuntu2204 \
  --admin-username azureuser \
  --generate-ssh-keys \
  --custom-data cloud-init.txt \
  --size Standard_B1s \
  --storage-sku Standard_LRS \
  --public-ip-sku Standard
```

**`From output of this command, retrive the public ip`**

## Open Port 80 (HTTP)

```bash
az vm open-port \
  --resource-group kml_rg_main-06c66b102d8744e8 \
  --name xfusion-vm \
  --port 80 \
  --priority 800
```

## Verify Nginx status

1. Enter <public-ip> to a browser to see Nginx welcome page.

   `http://<public-ip>:80`

   <img width="579" height="222" alt="image" src="https://github.com/user-attachments/assets/44e378bb-e884-4436-b82b-4609e074537c" />

1. Check via CLI using `curl`

   ```bash
   curl http://<public-ip>
   ```

   **Should return Nginx welcome page**

   <img width="1009" height="464" alt="image" src="https://github.com/user-attachments/assets/1fbd2419-0e21-48f4-8e16-ad9ae86f314e" />
   
1. SSH into VM from and check via cli

   ```bash
   ssh azureuser@<public-ip>
   ```

   ```bash
   sudo systemctl status nginx
   ```
   <img width="1038" height="272" alt="image" src="https://github.com/user-attachments/assets/1a4b4ee0-cd5f-45b0-80c3-51f4df629079" />

