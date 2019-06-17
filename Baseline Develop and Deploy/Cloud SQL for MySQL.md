# Cloud SQL for MySQL
[Manage PostgreSQL and MySQL Databases Easily with Cloud SQL](https://youtu.be/EQJK0tNW-g4)

## Objective
**Create and connect to a Google Cloud SQL MySQL instance and perform basic SQL operations using the Google Cloud Platform Console and the mysql client.**

## Steps
### **Create a Cloud SQL instance**
1. Click on the menu icon in the top left of the screen to see the Navigation menu.
2. In the left menu of the Console, click on SQL.
3. Click Create Instance.
4. Create your instance with the following settings:
    * Click MySQL, then Next.
    * Click Choose Second Generation.
    * Enter myinstance for Instance ID.
    * Enter a password for the root user. Save the password, you'll need it in the next section.
5. Use the default values for the other fields.
6. Click Create.

### **Connect to your instance using the mysql client in the Cloud Shell**
1. In the Google Cloud Platform Console, click the Cloud Shell icon in the upper right corner.
2. At the Cloud Shell prompt, connect to your Cloud SQL instance by running:
    ```sh
    gcloud sql connect myinstance --user=root
    ```
3. Enter your root password when prompted. Note: The cursor will not move.
4. Press Enter when you're done typing.

### ***Create a database and upload data***
1. Create a SQL database on your Cloud SQL instance:
    ```sql
    CREATE DATABASE guestbook;
    ```
2. Insert sample data into the guestbook database:
    ```sql
    USE guestbook;
    CREATE TABLE entries (guestName VARCHAR(255), content VARCHAR(255),
        entryID INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(entryID));
        INSERT INTO entries (guestName, content) values ("first guest", "I got here!");
    INSERT INTO entries (guestName, content) values ("second guest", "Me too!");
    ```
3. Retrieve the data:
    ```sql
    SELECT * FROM entries;
    ```