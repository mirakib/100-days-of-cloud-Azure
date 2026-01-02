# Day 31: Deploying and Managing a Web Application

The Nautilus DevOps team is tasked with deploying a Python-based web application on Azure. You need to create a web app using the following specifications:

1) The Web App name should be `xfusion-webapp`.
2) It should be created in the `West US` region under the `default` resource group.
3) The publish option should be set to Code.
4) The Runtime Stack should be `Python` with `Linux` as the operating system.
5) Create a new `App Service Plan` named `xfusion-learn-python` with the `SKU Basic B1`.
6) Application Insights should be disabled.
7) Add tags:

   - **Name**: WebAppLearning
   - **Environment**: Dev

Make sure the web app is in `Running` state after creation.


## Task 1: Create a new App Service Plan

1. From Azure portal, go to `All services` and select `Web & Mobile` from navigation pane.

   <img width="1342" height="560" alt="image" src="https://github.com/user-attachments/assets/7827d54f-5ce0-4cfb-b89e-c1fd37f322b4" />

2. From `Application management` section, select `App service` and click `+ Create` to select `Web app`.

   <img width="376" height="214" alt="image" src="https://github.com/user-attachments/assets/1ea4504a-dd7b-4772-a1a1-937e069fc90a" />

3. The Web App name should be `xfusion-webapp` and It should be created under the `default` resource group.

   <img width="979" height="284" alt="image" src="https://github.com/user-attachments/assets/613e951f-e279-40a0-8555-550443ae65a8" />

4. The publish option should be set to `Code` and `Runtime Stack` should be `Python` with `Linux` as the operating system.

   <img width="982" height="115" alt="image" src="https://github.com/user-attachments/assets/70ef40fd-5dfc-441b-96dd-6f78a573748b" />

5. It should be created in the `West US` region.

   <img width="975" height="88" alt="image" src="https://github.com/user-attachments/assets/aaf607f9-f718-4038-93ac-0278cbf6e3fc" />

7. Create a new `App Service Plan` named `xfusion-learn-python` with the `SKU Basic B1`.

   <img width="977" height="195" alt="image" src="https://github.com/user-attachments/assets/d21a29a0-0f31-41dd-9313-db19599c1387" />

8. On the `Monitor + secure` tab, check **Application Insights** as `No`.

   <img width="978" height="272" alt="image" src="https://github.com/user-attachments/assets/1989718c-468f-4cdd-b6f5-e1d942c9e86f" />

9. On the `Tag` tab, Add tags:

    <img width="978" height="273" alt="image" src="https://github.com/user-attachments/assets/b0bfddce-4f9d-427c-88d5-c2ca50a8dbf1" />

10. On the `Review + create` tab, click on `Create`.

11. Make sure the web app is in `Running` state after creation.

    <img width="1107" height="394" alt="image" src="https://github.com/user-attachments/assets/4074ff9d-e828-4788-9ffd-7cde5fab7d1e" />
