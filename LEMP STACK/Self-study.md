# LEMP STACK SELF-STDUY- STEGHUB DEVOPS TRAINING

# Learnt: SQL commands and Nano Editor for Linux

## Basic SQL Syntax and Common Commands

To enhance your DevOps and Cloud Engineering skills, it's crucial to be familiar with SQL. Here's a quick guide to get you started:

### Common SQL Commands

- **SELECT**: Used to select data from a database.
  ```sql
  SELECT column1, column2 FROM table_name;
  ```

- **INSERT**: Used to insert new data into a database.
  ```sql
  INSERT INTO table_name (column1, column2) VALUES (value1, value2);
  ```

- **UPDATE**: Used to modify existing data in a database.
  ```sql
  UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
  ```

- **DELETE**: Used to delete data from a database.
  ```sql
  DELETE FROM table_name WHERE condition;
  ```

- **CREATE TABLE**: Used to create a new table.
  ```sql
  CREATE TABLE table_name (
   column1 datatype,
   column2 datatype,
   ...
  );
  ```

- **DROP TABLE**: Used to delete a table.
  ```sql
  DROP TABLE table_name;
  ```

## Basic SQL Syntax

SQL statements typically follow a simple structure:

  ```sql
  SELECT column1, column2
  FROM table_name
  WHERE condition;
  ```

## Text Editors: VIM and Nano

### VIM

VIM is a powerful text editor widely used in the DevOps and Cloud Engineering field. Here are some basic commands:

- **Insert Mode**: Press `i` to enter Insert mode.
- **Save and Quit**: Press `Esc`, then type `:wq` and press `Enter`.
- **Quit Without Saving**: Press `Esc`, then type `:q!` and press `Enter`.

### Nano

Nano is a simpler, user-friendly text editor. Here are some basic commands:

- **Open a File**:
  ```sh
  nano filename
  ```

- **Save Changes**: Press `Ctrl + O`, then `Enter`.

- **Exit Nano**: Press `Ctrl + X`.

### Basic Nano Commands

- **Cut Text**: `Ctrl + K`
- **Paste Text**: `Ctrl + U`
- **Search Text**: `Ctrl + W`
- **Go to Line**: `Ctrl + _`
- **Move up**: Ctrl + P 
- **Move down**: Ctrl + n
- **Going to the begiining of a line**: `Ctrl + a`
- **Going to the end of a line**: `Ctrl + e`

By default Linux Operating System has three editors namely nano, vim, and emacs. It is paramount to have a knowledge of atleast two for ease of work life.