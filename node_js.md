Here are the steps to follow:

1. Set up the environment: First, you need to install Node.js on your system. Once installed, create a new directory for your project and open a command prompt in that directory.

2. Install dependencies: You need to install the necessary dependencies for your project. For this tutorial, we'll be using the `express` package as our web framework and the `mysql` package for interacting with a MySQL database. You can install both using the following command:

   ```
   npm install express mysql
   ```

3. Create a database: For this tutorial, we'll be using a MySQL database. You can create a new database by running the following command in your MySQL command prompt:

   ```
   CREATE DATABASE testdb;
   ```

4. Create a table: Next, you need to create a table in your database. For this tutorial, we'll be creating a simple `users` table with three columns - `id`, `name`, and `email`. You can create the table using the following command:

   ```
   CREATE TABLE users (
     id INT(11) NOT NULL AUTO_INCREMENT,
     name VARCHAR(50) NOT NULL,
     email VARCHAR(50) NOT NULL,
     PRIMARY KEY (id)
   );
   ```

5. Set up the server: Now that your database is set up, you need to set up your Node.js server. Create a new file called `server.js` in your project directory and add the following code:

   ```javascript
   const express = require('express');
   const mysql = require('mysql');
   
   const app = express();
   
   // Set up MySQL connection
   const db = mysql.createConnection({
     host: 'localhost',
     user: 'root',
     password: '',
     database: 'testdb'
   });
   
   // Connect to MySQL
   db.connect((err) => {
     if (err) {
       throw err;
     }
     console.log('Connected to MySQL database');
   });
   
   // Start server
   app.listen(3000, () => {
     console.log('Server started on port 3000');
   });
   ```

   This code sets up an Express app and creates a connection to your MySQL database. The app listens on port 3000 for incoming requests.

6. Define routes: Next, you need to define routes for your API. Add the following code to `server.js`:

   ```javascript
   // Get all users
   app.get('/users', (req, res) => {
     const sql = 'SELECT * FROM users';
     db.query(sql, (err, result) => {
       if (err) {
         throw err;
       }
       res.send(result);
     });
   });
   
   // Get a single user
   app.get('/users/:id', (req, res) => {
     const sql = `SELECT * FROM users WHERE id = ${req.params.id}`;
     db.query(sql, (err, result) => {
       if (err) {
         throw err;
       }
       res.send(result);
     });
   });
   
   // Create a user
   app.post('/users', (req, res) => {
     const { name, email } = req.body;
     const sql = `INSERT INTO users (name, email) VALUES ('${name}', '${email}')`;
     db.query(sql, (err, result) => {
       if (err) {
         throw err;
       }
       res.send('User created successfully');
     });
   });
   
   // Update a user
   app.put('/users/:id', (req, res) => {
     const {     name, email } = req.body;
     const sql = `UPDATE users SET name = '${name}', email = '${email}' WHERE id = ${req.params.id}`;
     db.query(sql, (err, result) => {
       if (err) {
         throw err;
       }
       res.send('User updated successfully');
     });
   });
   
   // Delete a user
   app.delete('/users/:id', (req, res) => {
     const sql = `DELETE FROM users WHERE id = ${req.params.id}`;
     db.query(sql, (err, result) => {
       if (err) {
         throw err;
       }
       res.send('User deleted successfully');
     });
   });
   ```

   This code defines routes for getting all users, getting a single user by ID, creating a new user, updating an existing user, and deleting a user. Each route executes a SQL query on the `users` table and sends the result back to the client.

7. Test the API: You can now test your API using a tool like Postman. Start your server by running `node server.js` in your command prompt, and then send HTTP requests to the appropriate endpoints. For example:

   - GET all users: `http://localhost:3000/users`
   - GET a single user: `http://localhost:3000/users/1`
   - POST a new user: `http://localhost:3000/users` with body: `{ "name": "John Doe", "email": "johndoe@example.com" }`
   - PUT an existing user: `http://localhost:3000/users/1` with body: `{ "name": "Jane Doe", "email": "janedoe@example.com" }`
   - DELETE a user: `http://localhost:3000/users/1`

That's it! You now have a fully functional API for interacting with a MySQL database using Node.js.
