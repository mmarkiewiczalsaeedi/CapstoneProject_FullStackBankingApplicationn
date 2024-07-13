# MIT Emeritus Project 3: Full Stack Blissful Bank Application

## Project Title
Full Stack Blissful Bank Application

## Description/Motivation
The Full Stack Blissful Bank Application is designed to simulate a banking system, allowing users to create accounts and manage their balances. This project helps users understand the fundamental operations of a bank and serves as a practical exercise in building a full stack web application using the MERN stack (MongoDB, Express, React, Node.js).

## Installation Guidelines

### Server Setup
1. **Initialize Node.js project:**
    ```bash
    npm init -y
    ```
2. **Install required packages:**
    ```bash
    npm i express mongoose dotenv cors mongodb axios
    ```
3. **MongoDB Atlas:**
    - Create a cluster.
    - Obtain the connection URI and follow the instructions provided by MongoDB.
    - Add the URI to a `.env` file in the server directory:
      ```plaintext
      MONGODB_URI=<your_mongodb_uri>
      ```
    - Add `.env` to `.gitignore` in the backend directory.
    - In the cluster's security settings, allow all network access and set database access to read and write.

### Express Server
1. **Create an Express app and connect to MongoDB:**
    ```javascript
    const express = require('express');
    const mongoose = require('mongoose');
    const dotenv = require('dotenv');
    const cors = require('cors');

    dotenv.config();
    const app = express();
    app.use(cors());

    mongoose.connect(process.env.MONGODB_URI, { useNewUrlParser: true, useUnifiedTopology: true });

    app.listen(3000, () => {
      console.log('Running on port 3000');
    });
    ```

### MongoDB Models and Data Access Layer (DAL)
1. **Define MongoDB schemas in the `models` directory.**
2. **Create DAL functions or classes to handle database operations.**
3. **Set the entry point in `package.json`:**
    ```json
    "start": "node server/app.js",
    ```

### Seeding the Database
1. **Create a `seed.js` file to populate the database with initial data:**
    ```javascript
    // Example seed.js content
    const mongoose = require('mongoose');
    const User = require('./models/user');
    
    mongoose.connect(process.env.MONGODB_URI, { useNewUrlParser: true, useUnifiedTopology: true });

    const seedUsers = async () => {
      const users = [
        { name: 'John Doe', email: 'john@example.com', balance: 100 },
        { name: 'Jane Smith', email: 'jane@example.com', balance: 200 }
      ];
      await User.insertMany(users);
      console.log('Database seeded!');
    };

    seedUsers().then(() => mongoose.disconnect());
    ```

### Starting the Application
1. **Set the proxy in `client/package.json`:**
    ```json
    "proxy": "http://localhost:5001"
    ```
2. **Install dependencies in both client and server directories:**
    ```bash
    npm install
    ```
3. **Seed the database:**
    ```bash
    node seed.js
    ```
4. **Start the application in both client and server directories:**
    ```bash
    npm start
    ```

### Serving Static Files and Heroku Deployment
1. **Serve static files from the React app in `app.js`:**
    ```javascript
    const path = require('path');
    app.use(express.static(path.join(__dirname, '../client/build')));
    ```
2. **Add a Heroku post-build script to `server/package.json`:**
    ```json
    "heroku-postbuild": "cd ../client && npm install && npm run build"
    ```
3. **Create a `Procfile` for Heroku:**
    ```plaintext
    web: node server/app.js
    ```
4. **Set up Heroku deployment:**
    ```bash
    heroku login
    heroku create
    git init
    heroku git:remote -a <your-heroku-app-name>
    git add .
    git commit -am "initial"
    git push heroku main
    heroku config:set MONGODB_URI=<your_mongodb_uri>
    heroku open
    ```

## Improvements
- Created a `server/models` folder to better organize the relationship between DAL and models.
- The DAL focuses on database operations and connectivity, using Mongoose models for CRUD operations.
- The models directory houses Mongoose schema definitions for structured data handling.

## Conclusion
By organizing the application in this manner, the following benefits are achieved:
- **Clarity:** Clear separation between schema definitions and database operations.
- **Maintainability:** Improved code readability and reusability.
- **Scalability:** The structure scales well with the application's growth.

## Features
- User account creation and management.
- Balance tracking for each user.
- Interactive UI for account operations.

## Technology Stack
- **Frontend:** React
- **Backend:** Node.js, Express
- **Database:** MongoDB, Mongoose
- **Deployment:** Heroku

## License
This project is licensed under the MIT License.

## Submission Instructions
Submit a link to your GitHub README.

## Screenshots
![Screenshot](path/to/your/screenshot.png)
```
