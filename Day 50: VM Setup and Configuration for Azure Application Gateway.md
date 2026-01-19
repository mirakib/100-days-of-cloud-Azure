# Day 50: VM Setup and Configuration for Azure Application Gateway

The Nautilus DevOps team needs to set up an Azure Application Gateway to manage traffic for a backend pool of virtual machines. The gateway will serve as a load balancer, distributing traffic across the VMs.
Task:

1) **Azure Virtual Network and Subnet:**

    - Create a Virtual Network (VNet) named `datacenter-vnet` in the `East US` region.
    - Create a Subnet named `datacenter-subnet` within the VNet for the VMs.
    - Create a Subnet named `datacenter-apgw-subnet` within the VNet for the Application Gateway.

2) **Azure Virtual Machines:**

    - Create two VMs named `datacenter-vm1` and `datacenter-vm2` in the `East US` region.
    - Install `Nginx` on both VMs.
    - Configure `index.html` on VM1 to display "**Welcome to KKE Labs:Version 1**".
    - Configure `index.html` on VM2 to display "**Welcome to KKE Labs:Version 2**".

3) **Azure Application Gateway:**

    - Create an Application Gateway named `datacenter-apgw` in the `East US` region.
    - Assign the `datacenter-apgw-subnet` to the Application Gateway.
    - Create a frontend IP configuration named `datacenter-apgw-ip`.
    - Add the VMs `datacenter-vm1` and `datacenter-vm2` to the backend pool.
    - Configure a basic routing rule to distribute traffic between the VMs.

4) **Validation:**

    - Verify that the Application Gateway distributes traffic to both VMs.
    - Ensure that accessing the Application Gateway URL displays either "**Welcome to KKE Labs:Version 1**" or "**Welcome to KKE Labs:Version 2**" depending on the load balancing.




## Task 1: Create Virtual Network and Subnets

1. **Open Azure Portal → Virtual networks → Create and create VNet datacenter-vnet in East US**

   <img width="1329" height="202" alt="image" src="https://github.com/user-attachments/assets/cd5027d8-f278-4dc1-bcaf-b9497c4f9a94" />

2. **Add subnet datacenter-subnet (e.g., 10.0.1.0/24) for virtual machines**

   <img width="523" height="579" alt="image" src="https://github.com/user-attachments/assets/b85009c6-641d-4e1a-8785-ff2b01f035cb" />

3. **Add subnet datacenter-apgw-subnet (e.g., 10.0.2.0/24) for Application Gateway**

   <img width="523" height="575" alt="image" src="https://github.com/user-attachments/assets/ee59b9b7-11a2-453e-b659-a8eec5d2c452" />

4. **Review subnets after creating.**

   <img width="653" height="300" alt="image" src="https://github.com/user-attachments/assets/b0f98bec-aa72-4e21-a721-b5e234ebefdc" />

## Task 2: Create Virtual Machines

1. **Create VM datacenter-vm1 in East US using datacenter-vnet / datacenter-subnet**

   <img width="1342" height="393" alt="image" src="https://github.com/user-attachments/assets/4074a23c-0afd-4712-8131-77e6e2b2da43" />

   <img width="1348" height="190" alt="image" src="https://github.com/user-attachments/assets/5c95afb8-d2a9-4c91-bede-3d7c47596122" />

   <img width="1348" height="434" alt="image" src="https://github.com/user-attachments/assets/cddb25cf-eace-4c0f-8109-75c498e1807b" />

2. **Create VM datacenter-vm2 in East US using datacenter-vnet / datacenter-subnet**

   <img width="1346" height="387" alt="image" src="https://github.com/user-attachments/assets/19a68376-2ed6-4dbf-8c19-1c4d0106408d" />

   <img width="1348" height="190" alt="image" src="https://github.com/user-attachments/assets/5c95afb8-d2a9-4c91-bede-3d7c47596122" />

   <img width="1348" height="434" alt="image" src="https://github.com/user-attachments/assets/cddb25cf-eace-4c0f-8109-75c498e1807b" />

## Task 3: Install Nginx and Configure Web Pages

1. **Install and setup Nginx on `datacenter-vm1`**

   ```sh
   sudo apt update
   sudo apt install nginx -y
   echo "Welcome to KKE Labs:Version 1" | sudo tee /var/www/html/index.html
   sudo systemctl restart nginx
   ```

2. **Install and setup Nginx on `datacenter-vm2`**

   ```sh
   sudo apt update
   sudo apt install nginx -y
   echo "Welcome to KKE Labs:Version 2" | sudo tee /var/www/html/index.html
   sudo systemctl restart nginx
   ```

## Task 4: Create Azure Application Gateway (Azure Portal)

1. **Open Azure Portal → Application Gateways → Create**

2. **Set name `datacenter-apgw`, region `East US`, and tier `Basic`**

   <img width="1346" height="380" alt="image" src="https://github.com/user-attachments/assets/6b18c14b-0a7a-4c8f-ae19-217a73768fe7" />

3. **Assign VNet datacenter-vnet and subnet `datacenter-apgw-subnet`**

   <img width="1346" height="174" alt="image" src="https://github.com/user-attachments/assets/d0c1b8b7-ebd5-404f-b6eb-85051771284b" />

4. **Create frontend IP configuration `datacenter-apgw-ip` (Public IPv4)**

   <img width="1365" height="485" alt="image" src="https://github.com/user-attachments/assets/323f0ce4-196f-4d99-89ed-c92dcbefda57" />

5. **Add backend pool containing private IPs of `datacenter-vm1` and `datacenter-vm2`**
   
   <img width="1365" height="438" alt="image" src="https://github.com/user-attachments/assets/0d1575b9-bb46-48e6-94f3-44f829914640" />

6. **Create HTTP listener on port `80` using `datacenter-apgw-ip`**

   <img width="764" height="574" alt="image" src="https://github.com/user-attachments/assets/d1f9f17e-8a2a-4397-a174-606f46cccd5a" />

7. **Create basic routing rule linking listener to backend pool**

   <img width="764" height="574" alt="image" src="https://github.com/user-attachments/assets/b91ce4ee-6a54-4e1b-bc3b-30aa9be3fe61" />

8. **Use default HTTP settings for load balancing**

   <img width="1365" height="438" alt="image" src="https://github.com/user-attachments/assets/c15cd898-9d02-4cfd-8e52-a8f20f2c3284" />


## Task 5: Validation of the task

1. **Copy the public IP or DNS name of `datacenter-apgw`**

2. **Open the URL in a browser**

3. **Refresh multiple times to observe traffic switching between `Version 1` and `Version 2`**
