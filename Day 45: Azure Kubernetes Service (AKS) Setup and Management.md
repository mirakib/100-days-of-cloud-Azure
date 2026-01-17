# Day 45: Azure Kubernetes Service (AKS) Setup and Management

The Nautilus DevOps team is tasked with preparing an AKS cluster to deploy a Kubernetes-based application. The team has the following requirements:

- Create an AKS cluster named `devops-aks`.
- The Kubernetes version must be `1.33.0`.
- The AKS cluster endpoint access must be `private`.
- Ensure the cluster is created in the `Central US` region.
- Edit the `agentpool` Node pools (delete all other node pool if exists) and configure the cluster with the following properties:
  - Node size: `D2s v3`.
  - Minimum node count: `1`.
  - Maximum node count: `2`.

- Disable the Container Insights for now and disable all kind of monitoring as well.

The AKS cluster must be configured with high availability and private endpoint access. Verify that the cluster meets the requirements and is ready for workloads.

## Task 1: Create an AKS cluster

1. **On the Azure portal home page, select `Create a resource`.**

   <img width="1064" height="160" alt="image" src="https://github.com/user-attachments/assets/f650fd61-fcc2-4bd9-b8de-51dedcdaa454" />

3. **In the Categories section, select `Infrastructure Services` > `Azure Kubernetes Service (AKS)`.**

   <img width="1328" height="430" alt="image" src="https://github.com/user-attachments/assets/81ab86ab-362a-4c01-9126-9a3365094dd8" />

4. **On the `Basics` tab, configure the following settings:**

   <img width="1350" height="431" alt="image" src="https://github.com/user-attachments/assets/544c3020-fd86-4c48-888f-6221be63e9f6" />

5. **Set Kubernetes version to `1.33.0`.**

   <img width="1351" height="284" alt="image" src="https://github.com/user-attachments/assets/d7433b71-9c33-4827-90a5-3507b19aad3d" />

6. **On the Node pools tab, ensure you have `agentpool` under Nodepool.**

   <img width="1344" height="248" alt="image" src="https://github.com/user-attachments/assets/432c5609-b333-461e-87ae-3483f33bafe4" />

7. **Configure the cluster with the following properties:**

    **Node size**: `D2s v3`.
   
    **Minimum node count**: `1`.
   
    **Maximum node count**: `2`.

   <img width="1346" height="308" alt="image" src="https://github.com/user-attachments/assets/c32c58b5-dc8b-4097-849a-a6a6cc3ebffb" />

9.  **On the `Networking` tab, make the AKS cluster endpoint access as private.**

    <img width="1242" height="497" alt="image" src="https://github.com/user-attachments/assets/deb2c3d6-1de1-4ec4-aaf8-d492553fb137" />

10. **On the `Monitoring` tab, Disable the Container Insights for now and disable all kind of monitoring as well.**

    <img width="1365" height="497" alt="image" src="https://github.com/user-attachments/assets/4887f0d7-999c-492d-9deb-dc569d89154d" />

11. **Select `Review + create` to run validation on the cluster configuration. After validation completes, select `Create`.**

    <img width="1365" height="497" alt="image" src="https://github.com/user-attachments/assets/1e135b4c-fa0c-45cb-b11b-e8276f4ec495" />

12. **It takes a few minutes to create the AKS cluster.**

    <img width="1097" height="272" alt="image" src="https://github.com/user-attachments/assets/de9d6f0d-e642-4885-8bff-fa77b0bf43af" />
