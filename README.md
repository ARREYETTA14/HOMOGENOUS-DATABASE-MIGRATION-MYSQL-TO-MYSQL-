# HOMOGENOUS-DATABASE-MIGRATION-MYSQL-TO-MYSQL-

![Homogenous_Migration_MySQL_to_MySQL-20240721-205155](https://github.com/user-attachments/assets/bf23e688-bf59-4182-b116-f1bf904bbf9b)

This project involves migrating a MySQL database within the same AWS region and VPC. The migration process is structured to ensure a smooth and efficient data transfer from the source database to the target database. The steps include setting up security groups, creating both source and target database instances, creating tables and inserting data, and performing the migration using MySQL Workbench. Here’s a detailed step-by-step guide to accomplish this migration:

**1.** Create 1 security group for the two databases

- That allows traffic for my IP

![image-20240721-193054](https://github.com/user-attachments/assets/65d4ad33-74ba-4ff3-ba2a-9559f84931df)

**2.** Create the Source Database Instance

- In the AWS Management Console, navigate to RDS.

![image-20240721-193754](https://github.com/user-attachments/assets/dac9475e-1509-44c1-b1b0-6d538232a9e6)

- Click "database" on the left pane then "Create database".

![image-20240721-194131](https://github.com/user-attachments/assets/ac1dda8f-8f22-46ae-a665-01430a10d732)

- Choose “Standard Create” then “MySQL”

![image-20240721-194231](https://github.com/user-attachments/assets/74eef615-2e6c-4036-87d3-6f34298add68) 

- Choose “Free Tier”

![image-20240721-194347](https://github.com/user-attachments/assets/2006e5fb-8067-441f-a5df-cb2de7b2180f)

- Fill in the “DB Instance Identifier”, Pass “Master Username” and choose “Self-managed”

![image-20240721-194505](https://github.com/user-attachments/assets/14e2b144-8e4a-4367-b746-af32f480fef2)

- Pass in the “Master Password”. It should be a strong Password.

![image-20240721-194610](https://github.com/user-attachments/assets/24bc7231-982e-4565-a3eb-a2f83f6a4ace)

- Leave rest as default then navigate to “Public access” and accept then choose the source database security group at the level of the security group.

![image-20240721-194721](https://github.com/user-attachments/assets/a8f86945-fa05-4da8-9d26-d37fad2ba8c2)

-  Leave the rest as default then create the Source Database.

**3.** Create the Target Database:

- A similar procedure as the above just needs to pass the right “Security group”. 

**4.** Connect to the Source Database, create a Table and insert data.

- Launch MySQL Workbench on your computer.

![image-20240721-195028](https://github.com/user-attachments/assets/6e104a83-b576-48fd-a4bf-556d934354cc)

-Clicking the "+" button to create a new connection, enter the necessary connection details (hostname, port, username, password, etc.), and then click "Test Connection" to ensure it's working. Once done, click  "OK" to save and open the connection.

**Hostname:** Pass database endpoint
**Username:** Pass Master Username
**Connection Name:** Any name of your choice

![image-20240721-195310](https://github.com/user-attachments/assets/4a9e2746-2255-4d5c-8fae-ecaa40d4802f)

- Click on Connection Made to access “Source database

![image-20240721-195420](https://github.com/user-attachments/assets/757bb291-d056-44da-9453-2952e2bcd57f)

-In the new SQL query tab, enter the following SQL command to create the source_db database:
  ```sh
  CREATE DATABASE source_db;
  ```
Execute the command by clicking the "Execute" button (lightning bolt icon) in the toolbar or by pressing Ctrl+Enter (Windows/Linux) or Cmd+Enter (Mac). You will get a green tick at the bottom showing it has been created.

![image-20240721-195819](https://github.com/user-attachments/assets/e0af2adc-344e-4bb6-a289-4812395b6934)

- Now, enter the following SQL command to create the ‘employees’ table:
  ```sh
    CREATE TABLE employees (
      id INT AUTO_INCREMENT PRIMARY KEY,
      name VARCHAR(50),
      position VARCHAR(50),
      salary DECIMAL(10, 2)
  );
  ```
- Finally, insert some sample data into the ‘employees’ table with the following SQL command:
  ```sh
  INSERT INTO employees (name, position, salary) VALUES
  ('Alice Johnson', 'Manager', 75000.00),
  ('Bob Smith', 'Developer', 60000.00),
  ('Charlie Brown', 'Designer', 55000.00);
  ```
- To ensure that the data has been inserted correctly, run a **‘SELECT’** query:
  ```sh
  SELECT * FROM employees;
  ```
![image-20240721-200352](https://github.com/user-attachments/assets/1b01a025-0935-4c95-8a8b-145c2969712f)

**5.** Connect to the Target Database via the MySQL workbench just as it was done for the Source Database.

- Run the following SQL commands to create the destination database and a similar table structure(schema) as in the Source Database:
  ```sh
  CREATE DATABASE destination_db;
  USE destination_db;
  
  CREATE TABLE employees (
      id INT AUTO_INCREMENT PRIMARY KEY,
      name VARCHAR(50),
      position VARCHAR(50),
      salary DECIMAL(10, 2)
  );
  ```
![image-20240721-200727](https://github.com/user-attachments/assets/a5b340bb-1f96-43d9-a066-791db2b811d4)



  
