# MERN Stack Implementation

## Overview 

### This project is aimed at implementing a web solution based on MERN stack in AWS cloud.

## Components

### This stack consists of four softwares, namely:
- MongoDB: This is a **No-SQL db** used to store application data in a form of documents
- ExpressJS: A **Server side** Web App framework for NodeJS.
- ReactJS: A **Frontend** framework developed by Facebook, and it is based on javascript and used to make UI components
- NodeJS: A javascript **runtime** environmen, used to run Javascript on a **machine** rather than in a browser


## Setting up the ec2 instance

1. Lauch an ec2 instance:
   - Sign in to AWS
   - Navigate to ec2 dashboard
   - Click on 'Launch instance' and choose ubuntu server 20.04 LTS as OS
  
2. Set instance details
3. Set storage
4. Add tags (optional)
5. Security setup:
   - Create a new security setup or use and existing one.
   - Allow inbound traffic on port 80(HTTP), 433(HTTPS), and port 22(SSH) from your IP address
6. Review and launch instance
7. Connect to the instance from your terminal (SSH into it as shown below):

## Backend  Config

1. Update ubuntu using the code below:
`sudo apt update`

2. Upgrade ubuntu:
`sudo apt upgrade`

3. Install NodeJS on the server
`sudo apt-get install -y nodejs`
### The command above install both nodejs and npm (a package manger for Node; like apt for ubuntu)

4. Verify installations
`node -v`
`npm -v`

5. Application setup
   - create a new dir for your To-do project:
     `mkdir Todo`
   - Then verify the Todo dir is created
     `ls`
   - change your directory to the Todo
     `cd Todo`
   - Run the command below to initialise your project
     `npm init`


## Installing ExpressJS

### As stated earlier, ExpressJS is a framework for NodeJS

1. Install it using:
   `npm install express`
2. Create a file index.js using the command below:
   `touch index.js`
3. verify that the file is created using `ls`
4. install the dotenv module using `npm install dotenv`
5. Open the inde.js file with this command to be able to perform operations inside:
   `vim index.js`
6. Input the following code into the file:
```JavaScipt
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
  console.log(`Server running on port ${port}`);
});
```

7. Start the server to see if it works:
    `node index.js`
8. 





