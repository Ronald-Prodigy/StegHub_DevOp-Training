# MERN WEB STACK IMPLEMENTATION


# Step 0 - Preparing Prerequisites

In order to complete this project, you will need an AWS account and a virtual server with Ubuntu Server OS.

## Setting Up an AWS Account and EC2 Instance

### If you do not have an AWS account:
Go back to **Project 1 Step 0** to sign in to the AWS free tier account and create a new EC2 Instance of `t2.micro` family with Ubuntu Server 24.04 LTS (HVM) image. Remember, you can have multiple EC2 instances, but make sure you **STOP** the ones you are not working with at the moment to save available free hours.

### Creating an EC2 Instance

1. **Navigate to the EC2 Dashboard** in your AWS Management Console.
2. **Click on "Launch Instance"**.
3. **Select the Ubuntu Server 24.04 LTS (HVM) image**.
4. **Choose the t2.micro instance type**.
5. **Configure instance details**, add storage, and configure security groups as needed.
6. **Add Tags**:
   - Key: `Name`
   - Value: Corresponds to the current project you are working on (e.g., "Project X Server")

### Example Tag Configuration
```text
Key: Name
Value: Project X Server
```

![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/ffcd9c76-2473-4af3-9a56-8519e3dfb384)

## Connecting to Your EC2 Instance

### Hint #1: Tagging Your Instances
When you create your EC2 Instances, you can add the Tag `Name` to it with a value that corresponds to the current project you are working on. This tag will be reflected in the name of the EC2 Instance.

### Hint #2 (for Windows users only): Using Windows Terminal
In previous projects, we used Putty and Git Bash to connect to our EC2 Instances. In this project and going forward, we are going to explore the usage of Windows Terminal.

### Steps to Connect Using Windows Terminal

1. **Download and Install Windows Terminal** from the Microsoft Store if you haven't already.
2. **Launch Windows Terminal**.
3. **Open a new tab with PowerShell or Command Prompt**.
4. **Connect to your EC2 Instance using SSH**:
   ```sh
   ssh -i "path/to/your-key.pem" ubuntu@your-ec2-public-ip
   ```

Replace `"path/to/your-key.pem"` with the path to your private key file and `your-ec2-public-ip` with the public IP address of your EC2 instance.

### Example Command
```sh
ssh -i "C:/Users/YourName/keys/my-key.pem" ubuntu@123.45.67.89
```


# Step 1 - Backend Configuration

## Update and Upgrade Ubuntu

First, update your package index and upgrade your system:

```sh
sudo apt update
sudo apt upgrade
```
![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/5a9a8672-69f5-482d-85d8-1f9f6acd63e0)

## 1.1 Install Node.js

Let's get the location of Node.js software from Ubuntu repositories:

```sh
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```
![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/ddcbf17b-71fa-441c-8776-d748a1c02c88)

Install Node.js on the server:

```sh
sudo apt-get install -y nodejs
```
![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/c534596f-6206-4d87-be81-7e3f52eb0e9d)

> **Note:** The command above installs both `nodejs` and `npm`. `npm` is a package manager for Node.js similar to `apt` for Ubuntu. It is used to install Node.js modules & packages and to manage dependency conflicts.

Verify the Node.js installation:

```sh
node -v
```
![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/469dbeef-bd14-474d-b456-e641f484d601)

Verify the npm installation:

```sh
npm -v
```
![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/2a5b76b3-dc06-4135-ab15-429519b70fa9)

## Application Code Setup

Create a new directory for your To-Do project:

```sh
mkdir Todo
```

Run the command below to verify that the `Todo` directory is created:

```sh
ls
```
![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/cef05190-f775-405a-aad1-25fa4591fb6d)

> **TIP:** In order to see some more useful information about files and directories, you can use the following combination of keys: `ls -lih`. It will show you different properties and sizes in a human-readable format. You can learn more about different useful keys for the `ls` command with `ls --help`.

Change your current directory to the newly created one:

```sh
cd Todo
```

Next, initialize your project with npm to create a `package.json` file. This file will contain information about your application and the dependencies that it needs to run. Follow the prompts after running the command. You can press `Enter` several times to accept default values, then accept to write out the `package.json` file by typing `yes`.

```sh
npm init
```

Run the command `ls` to confirm that you have the `package.json` file created:

```sh
ls
```

You should see the `package.json` file listed in the output.

![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/f3c3abe1-3775-41f6-928a-325a8a209b4e)



# Step 1.2 - Installing ExpressJS

Express is a framework for Node.js that simplifies development by abstracting a lot of low-level details. For example, Express helps define routes of your application based on HTTP methods and URLs.

## Install Express

To use Express, install it using npm:

```sh
npm install express
```
![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/f4dba715-db97-47ee-a111-fe341f6b686f)

## Create `index.js`

Now create a file `index.js` with the command below:

```sh
touch index.js
```

Run `ls` to confirm that your `index.js` file is successfully created.

![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/c654235d-5be6-4939-b15d-86a01a44fe92)

## Install dotenv Module

Install the `dotenv` module to manage environment variables:

```sh
npm install dotenv
```
![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/3231dc6d-9359-4944-8977-2a0b54e60818)

## Edit `index.js`

Open the `index.js` file with the command below:

```sh
nano index.js
```

Type the code below into it and save. Do not get overwhelmed by the code you see. For now, simply paste the code into the file.

```javascript
const express = require('express');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

app.use((req, res, next) => {
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
    next();
});

app.use((req, res, next) => {
    res.send('Welcome to Express');
});

app.listen(port, () => {
    console.log(`Server running on port ${port}`)
});
```

Notice that we have specified to use port `5000` in the code. This will be required later when we go on the browser.

Use `Ctrl`+`O` and press `ENTER` to save in nano and use `Ctrl`+`X` to exit nano.

## Start the Server

Now it is time to start our server to see if it works. Open your terminal in the same directory as your `index.js` file and type:

```sh
node index.js
```

If everything goes well, you should see `Server running on port 5000` in your terminal.

![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/b1affde8-e667-4e1a-8cec-bee636f252a4)

## Open Port 5000 in EC2 Security Groups

Now we need to open this port in EC2 Security Groups. Refer to **Project 1 Step 1 – Installing the Nginx Web Server**. There we created an inbound rule to open TCP port 80; you need to do the same for port 5000.

![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/126941f3-5391-4e65-9694-185e690fc88e)

## Access the Server

Open up your browser and try to access your server's Public IP or Public DNS name followed by port 5000:

```sh
http://<PublicIP-or-PublicDNS>:5000
```

### Quick Reminder: How to Get Your Server's Public IP and Public DNS Name

- You can find it in your AWS web console in EC2 details.
- Run `curl -s http://169.254.169.254/latest/meta-data/public-ipv4` for Public IP address or `curl -s http://169.254.169.254/latest/meta-data/public-hostname` for Public DNS name.

You should see `Welcome to Express` in your browser.

![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/4019ab14-7ba9-4bac-bdfc-ee72b27cc61f)

## Routes

There are three actions that our To-Do application needs to be able to do:
- Create a new task
- Display list of all tasks
- Delete a completed task

Each task will be associated with some particular endpoint and will use different standard HTTP request methods: `POST`, `GET`, `DELETE`.

For each task, we need to create routes that will define various endpoints that the To-Do app will depend on.

## Create Routes Directory

Let's create a folder `routes`:

```sh
mkdir routes
```

> **Tip:** You can open multiple shells in Putty or Linux/Mac to connect to the same EC2 instance.

Change directory to the `routes` folder:

```sh
cd routes
```

Now, create a file `api.js` with the command below:

```sh
touch api.js
```

Open the file with the command below:

```sh
nano api.js
```

Copy the code below into the file. (Do not be overwhelmed with the code):

```javascript
const express = require('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {
    // Code to get all todos
});

router.post('/todos', (req, res, next) => {
    // Code to create a new todo
});

router.delete('/todos/:id', (req, res, next) => {
    // Code to delete a todo
});

module.exports = router;
```
![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/6e766e69-3b38-4970-9402-64fdc8437cd8)

Save and exit the file.



# Step 1.3 - Models

Now comes the interesting part. Since the app is going to make use of MongoDB, which is a NoSQL database, we need to create a model.

A model is at the heart of JavaScript-based applications, and it is what makes them interactive.

We will also use models to define the database schema. This is important so that we can define the fields stored in each MongoDB document. This may seem like a lot of information, but don't worry, everything will become clear to you over time. I promise!

In essence, the Schema is a blueprint of how the database will be constructed, including other data fields that may not be required to be stored in the database. These are known as virtual properties.

## Install Mongoose

To create a Schema and a model, install Mongoose, which is a Node.js package that makes working with MongoDB easier.

Change directory back to the Todo folder:

```sh
cd ..
```

Install Mongoose:

```sh
npm install mongoose
```
![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/79ddd9e0-cc9e-4f10-9678-ffe7982d9969)

## Create the Models Directory and File

Create a new folder for models:

```sh
mkdir models
```

Change directory into the newly created `models` folder:

```sh
cd models
```

Inside the `models` folder, create a file named `todo.js`:

```sh
touch todo.js
```

> **Tip:** All three commands above can be defined in one line to be executed consecutively with the help of the `&&` operator, like this:
>
> ```sh
> mkdir models && cd models && touch todo.js
> ```

Open the file created with `nano todo.js`, then paste the code below into the file:

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

// Create schema for todo
const TodoSchema = new Schema({
    action: {
        type: String,
        required: [true, 'The todo text field is required']
    }
});

// Create model for todo
const Todo = mongoose.model('todo', TodoSchema);

module.exports = Todo;
```

Save and exit the file.

![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/37a57db0-4058-4bec-b5d3-c6117881e579)

## Update Routes to Use the New Model

We need to update our routes in the `api.js` file in the `routes` directory to make use of the new model.

Change directory to the `routes` directory:

```sh
cd ../routes
```

Open `api.js` with `nano api.js`, delete the existing code, and paste the code below into it:

```javascript
const express = require('express');
const router = express.Router();
const Todo = require('../models/todo');

router.get('/todos', (req, res, next) => {
    // This will return all the data, exposing only the id and action field to the client
    Todo.find({}, 'action')
        .then(data => res.json(data))
        .catch(next);
});

router.post('/todos', (req, res, next) => {
    if (req.body.action) {
        Todo.create(req.body)
            .then(data => res.json(data))
            .catch(next);
    } else {
        res.json({
            error: "The input field is empty"
        });
    }
});

router.delete('/todos/:id', (req, res, next) => {
    Todo.findOneAndDelete({ "_id": req.params.id })
        .then(data => res.json(data))
        .catch(next);
});

module.exports = router;
```
![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/c31892f7-324d-4839-b7f7-158cabc326a9)

Save and exit the file.



# 1.4 MongoDB Database

We need a database where we will store our data. For this, we will make use of mLab. mLab provides MongoDB database as a service solution (DBaaS), making it easier to manage our database.

## Sign Up for mLab

1. **Sign up for a shared clusters free account** [here](https://www.mongodb.com/cloud/atlas/register).
2. **Select AWS as the cloud provider** and choose a region near you.
3. **Complete the get started checklist**.

## Allow Access to the MongoDB Database

1. **Allow access from anywhere** (not secure, but ideal for testing).

   ![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/b9d2dc2c-9de3-4257-946f-379726b69629)

2. **IMPORTANT NOTE:** Change the deletion time from 6 Hours to 1 Week.

   ![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/0e91163f-536c-4c89-aa14-3a2f74509099)

## Create a MongoDB Database and Collection

1. **Create a new MongoDB database** and a collection inside mLab.

    ![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/831770c2-b0f4-4cc9-b46c-ba47b7fb2c46)

## Environment Variables

In the `index.js` file, we specified `process.env` to access environment variables, but we have not yet created this file. So we need to do that now.

1. **Create a file in your Todo directory and name it `.env`.**

    ```sh
    touch .env
    nano .env
    ```

2. **Add the connection string to access the database in it, just as below:**

    ```plaintext
    DB='mongodb+srv://<username>:<password>@<network-address>/<dbname>?retryWrites=true&w=majority'
    ```

    Ensure to update `<username>`, `<password>`, `<network-address>`, and `<dbname>` according to your setup.

    ![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/c06dc8a3-56df-44b3-9bb3-45dd2d4e7cf0)

## Update `index.js` to Use `.env`

1. **Open the file with vim:**

    ```sh
    nano index.js
    ```

2. **Delete the existing content:**

3. **Paste the entire code below:**

    ```javascript
    const express = require('express');
    const bodyParser = require('body-parser');
    const mongoose = require('mongoose');
    const routes = require('./routes/api');
    const path = require('path');
    require('dotenv').config();
    
    const app = express();
    
    const port = process.env.PORT || 5000;
    
    // Connect to the database
    mongoose.connect(process.env.DB)
        .then(() => console.log(`Database connected successfully`))
        .catch(err => console.log(err));
    
    // Override mongoose promise with node's promise
    mongoose.Promise = global.Promise;
    
    app.use((req, res, next) => {
        res.header("Access-Control-Allow-Origin", "*");
        res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
        next();
    });
    
    app.use(bodyParser.json());
    
    app.use('/api', routes);
    
    app.use((err, req, res, next) => {
        console.log(err);
        next();
    });
    
    app.listen(port, () => {
        console.log(`Server running on port ${port}`);
    });

    ```

Using environment variables to store information is considered more secure and a best practice to separate configuration and secret data from the application, instead of writing connection strings directly inside the `index.js` application file.

## Start Your Server

Start your server using the command:

```sh
node index.js
```
![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/4ea0417a-218f-4a11-81a2-75184eab0911)

You should see a message `Database connected successfully`. If so, we have our backend configured.


# 1.5 Testing Backend Code without Frontend using RESTful API

So far, we have written the backend part of our To-Do application and configured a database, but we do not have a frontend UI yet. We will need ReactJS code to achieve that. However, during development, we will need a way to test our code using RESTful API. Therefore, we will use an API development client to test our code.

In this project, we will use Postman to test our API. [Click here](https://www.postman.com/downloads/) to download and install Postman on your machine.

[Click here](https://learning.postman.com/docs/getting-started/introduction/) to learn how to perform CRUD operations on Postman.

You should test all the API endpoints and make sure they are working. For the endpoints that require a body, you should send JSON back with the necessary fields since it’s what we setup in our code.

## Testing with Postman

### Create a POST Request

Open Postman and create a POST request to the API:

```
http://<PublicIP-or-PublicDNS>:5000/api/todos
```

This request sends a new task to our To-Do list so the application can store it in the database.

> **Note:** Make sure you set the header key `Content-Type` as `application/json`.



**Example JSON body**:

```json
{
    "action": "Learn DevOps"
}
```
![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/5f6065dd-32a5-484c-a16e-94b0a043da54)

**Example Header**:

| Key           | Value             |
|---------------|-------------------|
| Content-Type  | application/json  |

![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/1be5771e-8657-401e-907e-a5c2032c409f)

### Create a GET Request

Create a GET request to your API:

```
http://<PublicIP-or-PublicDNS>:5000/api/todos
```
![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/d41c68a3-8bb4-4011-bdff-c4d8d12019ed)

This request retrieves all existing records from our To-Do application (backend requests these records from the database and sends them back as a response to the GET request).

### Create a DELETE Request (Optional Task)

To delete a task, you need to send its ID as part of the DELETE request. Create a DELETE request to your API:

```
http://<PublicIP-or-PublicDNS>:5000/api/todos/<taskID>
```

Replace `<taskID>` with the actual ID of the task you want to delete.

**Example**:

```
http://<PublicIP-or-PublicDNS>:5000/api/todos/60d21b4667d0d8992e610c85
```
![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/e5b544ea-f010-4491-87fe-87b3208b3e0b)

## Summary

By now we have tested the backend part of our To-Do application and have made sure that it supports all three operations we wanted:

- [x] **Display a list of tasks** - HTTP GET request
- [x] **Add a new task to the list** - HTTP POST request
- [x] **Delete an existing task from the list** - HTTP DELETE request

Using Postman, you can easily test and verify the functionality of your backend code without having a frontend UI in place.


# Step 2 - Frontend Creation

Since we are done with the functionality we want from our backend and API, it is time to create a user interface for a Web client (browser) to interact with the application via API. To start out with the frontend of the To-do app, we will use the `create-react-app` command to scaffold our app.

## Setting Up the React App

1. **Create React App**:
   In the same root directory as your backend code, which is the Todo directory, run:
   
   ```sh
   npm install -g yarn
   yarn create react-app client
   
   ```
   
   This will create a new folder in your Todo directory called `client`, where you will add all the React code.

   ![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/0cdd2e92-bf6c-41d5-9098-0a6b7a62c1fa)

## Running a React App

Before testing the React app, there are some dependencies that need to be installed.

1. **Install concurrently**:
   It is used to run more than one command simultaneously from the same terminal window.
   
   ```sh
   npm install concurrently --save-dev
   ```
   ![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/94e97685-b412-456b-886b-d963bc549b36)

2. **Install nodemon**:
   It is used to run and monitor the server. If there is any change in the server code, nodemon will restart it automatically and load the new changes.
   
   ```sh
   npm install nodemon --save-dev
   ```
   ![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/8e7ef021-5cc0-49ed-bca0-6b488eab1484)

3. **Update package.json**:
   In the Todo folder, open the `package.json` file. Change the `scripts` section and replace it with the code below:
   
   ```json
   "scripts": {
       "start": "node index.js",
       "start-watch": "nodemon index.js",
       "dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
   },
   ```

4. **Configure Proxy in package.json**:
   Change directory to `client`:
   
   ```sh
   cd client
   ```

   Open the `package.json` file:
   
   ```sh
   nano package.json
   ```

   Add the key-value pair in the `package.json` file:
   
   ```json
   "proxy": "http://localhost:5000"
   ```

   The whole purpose of adding the proxy configuration above is to make it possible to access the application directly from the browser by simply calling the server URL like `http://localhost:5000` rather than always including the entire path like `http://localhost:5000/api/todos`.

5. **Run the App**:
   Now, ensure you are inside the Todo directory, and simply run:
   
   ```sh
   npm run dev
   ```

   ![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/3dd614f8-7c1e-411d-b9e5-251bc464c996)

   Your app should open and start running on `http://localhost:3000`.

   ![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/1fd06a01-aa84-4741-83b0-e4891d1c34b0)

> **Important note**: In order to be able to access the application from the Internet, you have to open TCP port 3000 on EC2 by adding a new Security Group rule. You already know how to do it.

   ![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/41e93df4-af6c-4c25-bd7a-206153b61447)

By following these steps, you will have your frontend set up and running, ready to interact with your backend API.



# Step 2.1 - Creating Your React Components

One of the advantages of React is that it makes use of components, which are reusable and also make the code modular. For our Todo app, there will be two stateful components and one stateless component. 

## Setting Up the Components

1. **Navigate to the `client` directory**:
   
   ```sh
   cd client
   ```

2. **Move to the `src` directory**:

   ```sh
   cd src
   ```

3. **Create a `components` folder** inside the `src` folder:

   ```sh
   mkdir components
   ```

4. **Move into the `components` directory**:

   ```sh
   cd components
   ```

5. **Create the component files**:

   ```sh
   touch Input.js ListTodo.js Todo.js
   ```

### Creating the `Input` Component

1. **Open the `Input.js` file**:

   ```sh
   nano Input.js
   ```

2. **Copy and paste the following code into `Input.js`**:

   ```javascript
   import React, { Component } from 'react';
   import axios from 'axios';

   class Input extends Component {
       state = {
           action: ""
       }

       addTodo = () => {
           const task = { action: this.state.action }

           if(task.action && task.action.length > 0){
               axios.post('/api/todos', task)
                   .then(res => {
                       if(res.data){
                           this.props.getTodos();
                           this.setState({ action: "" });
                       }
                   })
                   .catch(err => console.log(err));
           } else {
               console.log('input field required');
           }
       }

       handleChange = (e) => {
           this.setState({ action: e.target.value });
       }

       render() {
           let { action } = this.state;
           return (
               <div>
                   <input type="text" onChange={this.handleChange} value={action} />
                   <button onClick={this.addTodo}>add todo</button>
               </div>
           );
       }
   }

   export default Input;
   ```

3. **Install Axios**:

   ```sh
   cd ../..
   npm install axios
   ```
   
   ![image](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/3837a5e5-e16c-47a7-8274-b510d9ae20bc)

### Creating the `ListTodo` Component

1. **Open the `ListTodo.js` file**:

   ```sh
   nano ListTodo.js
   ```

2. **Copy and paste the following code into `ListTodo.js`**:

   ```javascript
   import React from 'react';

   const ListTodo = ({ todos, deleteTodo }) => {
       return (
           <ul>
               {todos && todos.length > 0 ? (
                   todos.map(todo => (
                       <li key={todo._id} onClick={() => deleteTodo(todo._id)}>{todo.action}</li>
                   ))
               ) : (
                   <li>No todo(s) left</li>
               )}
           </ul>
       );
   }

   export default ListTodo;
   ```

### Creating the `Todo` Component

1. **Open the `Todo.js` file**:

   ```sh
   nano Todo.js
   ```

2. **Copy and paste the following code into `Todo.js`**:

   ```javascript
   import React, { Component } from 'react';
   import axios from 'axios';

   import Input from './Input';
   import ListTodo from './ListTodo';

   class Todo extends Component {
       state = {
           todos: []
       }

       componentDidMount() {
           this.getTodos();
       }

       getTodos = () => {
           axios.get('/api/todos')
               .then(res => {
                   if(res.data) {
                       this.setState({ todos: res.data });
                   }
               })
               .catch(err => console.log(err));
       }

       deleteTodo = (id) => {
           axios.delete(`/api/todos/${id}`)
               .then(res => {
                   if(res.data) {
                       this.getTodos();
                   }
               })
               .catch(err => console.log(err));
       }

       render() {
           let { todos } = this.state;
           return (
               <div>
                   <h1>My Todo(s)</h1>
                   <Input getTodos={this.getTodos} />
                   <ListTodo todos={todos} deleteTodo={this.deleteTodo} />
               </div>
           );
       }
   }

   export default Todo;
   ```

### Adjusting the `App` Component

1. **Move to the `src` directory**:

   ```sh
   cd ..
   ```

2. **Open the `App.js` file**:

   ```sh
   nano App.js
   ```

3. **Copy and paste the following code into `App.js`**:

   ```javascript
   import React from 'react';
   import Todo from './components/Todo';
   import './App.css';

   const App = () => {
       return (
           <div className="App">
               <Todo />
           </div>
       );
   }

   export default App;
   ```

### Adding CSS for the App

1. **Open the `App.css` file**:

   ```sh
   nano App.css
   ```

2. **Copy and paste the following code into `App.css`**:

   ```css
   .App {
       text-align: center;
       font-size: calc(10px + 2vmin);
       width: 60%;
       margin-left: auto;
       margin-right: auto;
   }

   input {
       height: 40px;
       width: 50%;
       border: none;
       border-bottom: 2px #101113 solid;
       background: none;
       font-size: 1.5rem;
       color: #787a80;
   }

   input:focus {
       outline: none;
   }

   button {
       width: 25%;
       height: 45px;
       border: none;
       margin-left: 10px;
       font-size: 25px;
       background: #101113;
       border-radius: 5px;
       color: #787a80;
       cursor: pointer;
   }

   button:focus {
       outline: none;
   }

   ul {
       list-style: none;
       text-align: left;
       padding: 15px;
       background: #171a1f;
       border-radius: 5px;
   }

   li {
       padding: 15px;
       font-size: 1.5rem;
       margin-bottom: 15px;
       background: #282c34;
       border-radius: 5px;
       overflow-wrap: break-word;
       cursor: pointer;
   }

   @media only screen and (min-width: 300px) {
       .App {
           width: 80%;
       }

       input {
           width: 100%;
       }

       button {
           width: 100%;
           margin-top: 15px;
           margin-left: 0;
       }
   }

   @media only screen and (min-width: 640px) {
       .App {
           width: 60%;
       }

       input {
           width: 50%;
       }

       button {
           width: 30%;
           margin-left: 10px;
           margin-top: 0;
       }
   }
   ```

3. **Open the `index.css` file**:

   ```sh
   nano index.css
   ```

4. **Copy and paste the following code into `index.css`**:

   ```css
   body {
       margin: 0;
       padding: 0;
       font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
       "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
       sans-serif;
       -webkit-font-smoothing: antialiased;
       -moz-osx-font-smoothing: grayscale;
       box-sizing: border-box;
       background-color: #282c34;
       color: #787a80;
   }

   code {
       font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
       monospace;
   }
   ```

### Running the App

1. **Move back to the Todo directory**:

   ```sh
   cd ../..
   ```

2. **Run the app**:

   ```sh
   npm run dev
   ```

   ![my pic](https://github.com/stiven-skyward/DevOpsTraining/assets/135337796/aefecfab-a105-4480-b1f4-03ff90b4de1c)

Assuming there are no errors when saving all these files, our To-Do app should be ready and fully functional with the functionality discussed earlier: creating a task, deleting a task, and viewing all your tasks.