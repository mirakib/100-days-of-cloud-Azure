# Day 30: Create Azure SQL Database

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to Azure. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. Recently, they started working on creating and configuring some database instances on Azure.

For this task, create one publicly accessible Azure SQL Database instance along with the following details:

1) The name of the Azure SQL Database must be `xfusion-sqldb`.

2) The server name must be `xfusion-server-17841`.

3) The compute + storage configuration should be **Basic (For less demanding workloads)**.

4) The backup storage redundancy should be **Locally-redundant backup storage**.

5) Set the login admin username to `xfusion-admin` and set an appropriate password.

6) Set the database size to `2 GiB`.

7) Keep the rest of the configurations as `default`. Finally, make sure the database is in the Ready state before submitting this task.


## To create a single database in the Azure portal:

1. Go to Azure SQL hub at aka.ms/azuresqlhub. In the pane for `Azure SQL Database`, select `Show options`.

   <img width="1070" height="453" alt="image" src="https://github.com/user-attachments/assets/3bf79c41-bbb9-412c-978d-c1c5c7367bcf" />

2. For `Database name`, enter `xfusion-sqldb`.

   <img width="979" height="189" alt="image" src="https://github.com/user-attachments/assets/3debe0b7-9b3d-4446-9085-f113fa8fb54b" />

3. For `Server`, select `Create new`.

   **Avoid resource location such as `eastus`, `southcentralus`, `centralus`, and `westus`**

   <img width="973" height="490" alt="image" src="https://github.com/user-attachments/assets/5f9e0c61-a4a5-4e8a-8ffd-de85697fd0ad" />

5. For `Authentication method`, select `Use SQL authentication` and enter username `xfusion-admin` and password as your choice.

   <img width="977" height="305" alt="image" src="https://github.com/user-attachments/assets/1b53e7fd-3f31-4d0e-b5fe-d636d1aa583c" />

6. The compute + storage configuration should be **Basic (For less demanding workloads)**.

   <img width="1348" height="460" alt="image" src="https://github.com/user-attachments/assets/8720bd86-c361-4ec8-855e-c011e1163556" />

7. The backup storage redundancy should be Locally-redundant backup storage.

   <img width="961" height="254" alt="image" src="https://github.com/user-attachments/assets/e37f08e7-e7ea-4d80-b477-4fd1d1546133" />

8. Keep the rest of the configurations as default.
9. Finally, make sure the database is in the `Ready` state.

    <img width="824" height="422" alt="image" src="https://github.com/user-attachments/assets/a1ea726a-f879-4971-8dc4-1eaff9343ff7" />

>[!Note]
> Check for the Status `Online` instead of `Ready` in overview.
