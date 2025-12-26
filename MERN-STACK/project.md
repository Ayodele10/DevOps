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

<img width="857" height="308" alt="image" src="https://github.com/user-attachments/assets/81c2a7ab-c2c3-4401-942d-3e5de96d26bf" />


## Backend  Config

1. Update ubuntu using the code below:
`sudo apt update`
<img width="690" height="185" alt="image" src="https://github.com/user-attachments/assets/682c4c49-22e1-4d28-a30b-14c8185930b4" />


2. Upgrade ubuntu:
`sudo apt upgrade`

3. Install NodeJS on the server
`sudo apt-get install -y nodejs`
### The command above install both nodejs and npm (a package manger for Node; like apt for ubuntu)
<img width="740" height="307" alt="image" src="https://github.com/user-attachments/assets/808c6f30-6b66-4869-b69b-d8be7847a532" />


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

<img width="721" height="424" alt="image" src="https://github.com/user-attachments/assets/d6dfe04a-c972-430a-883e-b486e2aabd16" />


## Installing ExpressJS

### As stated earlier, ExpressJS is a framework for NodeJS

1. Install it using:
   `npm install express`
2. Create a file index.js using the command below:
   `touch index.js`
3. verify that the file is created using `ls`

   <img width="646" height="356" alt="image" src="https://github.com/user-attachments/assets/680bf88b-68cd-47f0-9699-677b2e591ff9" />

4. install the dotenv module using `npm install dotenv`
   
   <img width="572" height="258" alt="image" src="https://github.com/user-attachments/assets/1d8238c6-0c39-41dd-82c4-7a96f79dfd1e" />

5. Open the index.js file with this command to be able to perform operations inside:
   `vim index.js`
6. Input the following code into the file:
```
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
<img width="518" height="746" alt="image" src="https://github.com/user-attachments/assets/7f471387-98be-4846-b337-442eef43f5c3" />

7. Start the server to see if it works:
    `node index.js`



## MODELS

A model is at the heart of JavaScript based applications, and it is what makes it interactive.

- Install Mongoose
  `npm install mongoose`
- create a new folder `mkdir models`, and enter into the directory
- create a file and name it todo.js `touch todo.js`
- Note: the previous 3 commands above can be runned by using && operator
  `mkdir models && cd models && touch todo.js`

  <img width="766" height="60" alt="image" src="https://github.com/user-attachments/assets/af70fcfe-67e8-41ba-b0e6-54f3c55015b7" />

- open the file with `vim todo.js` and paste the code below into it the file:
  const mongoose = require('mongoose');
const Schema = mongoose.Schema;

```JavaScript
const TodoSchema = new Schema({
  action: {
    type: String,
    required: [true, 'The todo text field is required']
  }
})

//create model for todo
const Todo = mongoose.model('todo', TodoSchema);

module.exports = Todo;

```

<img width="703" height="544" alt="image" src="https://github.com/user-attachments/assets/73b118cd-f1f4-4ce1-a314-0532438e34d7" />

- in the Routes directory, open api.js `vim api.js`, delete the code with `:%d` and paste the code below:
```JavaScript
const express = require('express');
const router = express.Router();
const Todo = require('../models/todo');

router.get('/todos', (req, res, next) => {

//this will return all the data, exposing only the id and action field 
//to the client
Todo.find({}, 'action')
.then(data => res.json(data))
.catch(next)
});

router.post('/todos', (req, res, next) => {
if(req.body.action){
Todo.create(req.body)
.then(data => res.json(data))
.catch(next)
}else {
res.json({
error: "The input field is empty"
})
}
});

router.delete('/todos/:id', (req, res, next) => {
Todo.findOneAndDelete({"_id": req.params.id})
.then(data => res.json(data))
.catch(next)
})

module.exports = router;
```

<img width="826" height="868" alt="image" src="https://github.com/user-attachments/assets/958f0e6c-bca8-4e51-8356-c401d8bacef8" />



