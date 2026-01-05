# Day 37: Setting Up MySQL on a Virtual Machine in Azure

The Nautilus DevOps team is tasked with integrating a PHP application hosted on an Azure VM with a MySQL database hosted on another Azure VM. This will validate the application's ability to connect to the database in the cloud.

**Create the MySQL VM:**
- Create a VM named `xfusion-mysql-vm` using the **MySQL Jetware** image from the Azure Marketplace.
- Configure the VM in the `East US` region.
- Use **Password** as the authentication type.
- Set the username as `xfusion_admin` and the password as `Namin@123456`.
- **Allow inbound traffic** on port `3306` to enable `MySQL` access.

**Setup the MySQL Database:**
- SSH into the `xfusion-mysql-vm`.
- Use the `sudo /jet/enter mysql` command to access the MySQL shell.
- Create a database named `xfusion_db`.
- Create a MySQL user named `xfusion_user` with password `password123`.
- Grant all privileges on the `xfusion_db` database to this user.

**PHP VM Setup:**
- A VM named `xfusion-php-vm` already exists in the `East US` region.
- This VM is hosting a PHP application and contains a pre-existing `db_test.php` file in the /var/www/html/ directory.

**Database Connection Configuration:**
- Retrieve the public IP address of the `xfusion-mysql-vm`.
- Update the database connection settings in the `db_test.php` file to use the MySQL credentials and public IP address of the `xfusion-mysql-vm`.

**Validation:**
- Access the `db_test.php` file from the `xfusion-php-vm` using its public IP address.
- Ensure the file displays the message Connected successfully, confirming the connection between the PHP application and the MySQL database.


Ensure the MySQL database allows inbound traffic on port `3306`.
Verify that the PHP application on the `xfusion-php-vm` successfully connects to the MySQL database on the `xfusion-mysql-vm`.

# Task 1: Create the MySQL VM

**1. Go to virtual machines dashboard and in the left menu, click `Virtual machines`.**

   <img width="248" height="395" alt="image" src="https://github.com/user-attachments/assets/6608d807-70a6-41b2-9583-ddd4f0a8a448" />

**2. Click `Create` → `Virtual machine`.**
**3. On the `Basic` tab, enter name and select region `East US`.**

   <img width="1350" height="351" alt="image" src="https://github.com/user-attachments/assets/df9881d7-9c00-49ce-84e0-02978a07c595" />

**4. On the `Basic` tab, Select the `MySQL Jetware` image from Azure Marketplace and `Standard_B1s` as `Size`.**

   <img width="1349" height="329" alt="image" src="https://github.com/user-attachments/assets/8b74a8a5-96fb-4b0c-846d-47d2f4bf39d3" />

**5. On the `Basic` tab, select `Authentication type` as `Password` and set the username as `xfusion_admin` and the password as `Namin@123456`.**

   <img width="1346" height="239" alt="image" src="https://github.com/user-attachments/assets/a1ebcd13-4a5d-41e9-90fa-e0f830c963df" />

**5. Next on the `Disks` tb, select `OS disk type` as `Standard HDD`.**

   <img width="1346" height="193" alt="image" src="https://github.com/user-attachments/assets/7bb2b78a-845e-4c14-a231-f56646531b88" />

**7. Next go top `Review + Create` and click `Create`.**

   <img width="560" height="419" alt="image" src="https://github.com/user-attachments/assets/416b2cd1-1ea3-4f3a-9ae2-1ce823a807b8" />

**8. Adjust inbound port rule for MySQL.**

   <img width="523" height="574" alt="image" src="https://github.com/user-attachments/assets/c4d2e825-cfed-4864-950c-8d6b56cb989e" />

**9. Review inbound port rules after adding.**

  <img width="1077" height="342" alt="image" src="https://github.com/user-attachments/assets/648c485e-3bae-4312-becc-91f6f8135b25" />


## Task 2: Setup the MySQL Database

**1. SSH into the xfusion-mysql-vm.**

   ```sh
   ssh xfusion_admin@<MYSQL_VM_PUBLIC_IP>
   ```
   
>[!Tip]
> Password: **Namin@123456**

**2. Enter into the MySQL Shell**

   ```sh
   sudo /jet/enter mysql
   ```

**3. Create a Database**

   ```sh
   CREATE DATABASE xfusion_db;
   ```

**4. Create a MySQL User**

   ```sh
   CREATE USER 'xfusion_user'@'%' IDENTIFIED BY 'password123';
   ```

**5. Grant Privileges**

   ```sh
   GRANT ALL PRIVILEGES ON xfusion_db.* TO 'xfusion_user'@'%';
   FLUSH PRIVILEGES;
   ```

**6. Exit MySQL shell**

   ```sh
   EXIT;
   ```

## Task 3: PHP VM Configuration (xfusion-php-vm)

**1. SSH into PHP VM from `azure-client` host**

   ```sh
   ssh azureuser@<PHP_VM_PUBLIC_IP>
   ```

**2. Edit `db_test.php` file.**
   
   ```sh
   cd /var/www/html/
   sudo nano db_test.php
   ```

**3. Update Database Credentials**

>[!IMPORTANT]
> Replace: `<MYSQL_VM_PUBLIC_IP>` with the actual public IP of `xfusion-mysql-vm`. Also `$username`, `$password`, `$dbname`.

  ```php
  <?php
    $servername = "<mysql-vm-public-ip>";
    $username = "xfusion_user";
    $password = "password123";
    $dbname = "xfusion_db";

    // Create connection
    $conn = new mysqli($servername, $username, $password, $dbname);

    // Check connection
    if ($conn->connect_error) {
      die("Connection failed: " . $conn->connect_error);
    }
    echo "Connected successfully";
  ?>
  ```

## Task 4: Validation

**1. On your local machine, open a browser and visit:**

   ```sh
   http://<PHP_VM_PUBLIC_IP>/db_test.php
   ```
   
**2. You should see `Connected successfully`**
