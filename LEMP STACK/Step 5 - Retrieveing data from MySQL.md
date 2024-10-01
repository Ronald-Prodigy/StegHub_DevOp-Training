# Step 6 - Retrieving Data from MySQL Database with PHP

In this step, you will create a test database (DB) with a simple "To do list" and configure access to it, so the Nginx website will be able to query data from the DB and display it.

At the time of this writing, the native MySQL PHP library `mysqlnd` doesn’t support `caching_sha2_authentication`, the default authentication method for MySQL 8. We’ll need to create a new user with the `mysql_native_password` authentication method to connect to the MySQL database from PHP.

We will create a database named `Student_Register` and a user named `Jefferey_John`, but you can replace these names with different values.

## Step 6.1: Create the Database and User

First, connect to the MySQL console using the root account:

    sudo mysql

To create a new database, run the following command from your MySQL console:

    CREATE DATABASE `Student_Register`;

![img](<create db.png>)

Now you can create a new user and grant them full privileges on the database you have just created.

The following command creates a new user named `Jefferey_John`, using `mysql_native_password` as the default authentication method. We’re defining this user’s password as `PassWord.1`, but you should replace this value with a secure password of your own choosing.

    CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';

Now we need to give this user permission over the `Student_Register` database:

    GRANT ALL ON example_database.* TO 'example_user'@'%';

This will give the `Jefferey_John` user full privileges over the `Student_Register` database while preventing this user from creating or modifying other databases on your server.

![img](<create user.png>)

Now exit the MySQL shell with:

    mysql> exit

## Step 6.2: Verify the New User

You can test if the new user has the proper permissions by logging in to the MySQL console again, this time using the custom user credentials:

    mysql -u Jefferey_John -p

Notice the `-p` flag in this command, which will prompt you for the password used when creating the `Jefferey_John` user. After logging in to the MySQL console, confirm that you have access to the `Student_Register` database:



    SHOW DATABASES;

This will give you the following output:

![img](<show database.png>)

## Step 6.3: Create a Test Table

Next, we’ll create a test table named `todo_list`. From the MySQL console, run the following statement:

    mysql> CREATE TABLE Student_Register.todo_list (
        item_id INT AUTO_INCREMENT,
        content VARCHAR(255),
        PRIMARY KEY(item_id)
    );

![img](<create table.png>)

Insert a few rows of content in the test table. You might want to repeat the next command a few times, using different values:

    INSERT INTO Student_Register.todo_list (content) VALUES ("My first important item");

To confirm that the data was successfully saved to your table, run:

    SELECT * FROM Student_Register.todo_list;

You’ll see the following output:

![img](<insert into.png>)

After confirming that you have valid data in your test table, you can exit the MySQL console:

    mysql> exit

## Step 6.4: Create a PHP Script to Retrieve Data

Now you can create a PHP script that will connect to MySQL and query for your content. Create a new PHP file in your custom web root directory using your preferred editor. We’ll use `nano` for that:

    nano /var/www/projectLEMP/todo_list.php

The following PHP script connects to the MySQL database, queries for the content of the `todo_list` table, and displays the results in a list. If there is a problem with the database connection, it will throw an exception.

Copy this content into your `todo_list.php` script:

    <?php
    $user = "Jefferey_John";
    $password = "PassWord.1";
    $database = "Student_Register";
    $table = "todo_list";

    try {
      $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
      echo "<h2>TODO</h2><ol>";
      foreach($db->query("SELECT content FROM $table") as $row) {
        echo "<li>" . $row['content'] . "</li>";
      }
      echo "</ol>";
    } catch (PDOException $e) {
        print "Error!: " . $e->getMessage() . "<br/>";
        die();
    }

Save and close the file when you are done editing.

## Step 6.5: Access the PHP Script

You can now access this page in your web browser by visiting the domain name or public IP address configured for your website, followed by `/todo_list.php`:

    http://<Public_domain_or_IP>/todo_list.php

You should see a page like this, showing the content you’ve inserted in your test table:

![img](<todo_list page.png>)

That means your PHP environment is ready to connect and interact with your MySQL server.