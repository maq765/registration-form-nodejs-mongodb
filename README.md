# registration-form-nodejs-mongodb
An application built with Node.js and MongoDB for user registration. Includes a registration form with fields for name, email, and password, allowing users to sign up and store their information securely.

To create a registration form that signs up users and stores their information using HTML, CSS, Node.js, and MongoDB, we have to follow these steps:

### Step 1: Set Up Your Project
1. **Create a new directory for your project**.
2. **Initialize a new Node.js project**:
    ```bash
    npm init -y
    ```

### Step 2: Install Required Dependencies
Install the necessary dependencies using npm:
```bash
npm install express mongoose body-parser ejs
```

### Step 3: Set Up Your Project Structure
Organize your project directory as follows:
```
/project-directory
    /public
        /css
            styles.css
    /views
        index.ejs
        register.ejs
    app.js
```

### Step 4: Create the HTML Form
Create `register.ejs` file in the `views` directory:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="/css/styles.css">
    <title>Registration Form</title>
</head>
<body>
    <h2>Registration Form</h2>
    <form action="/register" method="POST">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required><br><br>
        
        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required><br><br>
        
        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required><br><br>
        
        <input type="submit" value="Register">
    </form>
</body>
</html>
```

### Step 5: Create a CSS File
Create `styles.css` file in the `public/css` directory:
```css
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 20px;
    background-color: #f0f0f0;
}

form {
    background: #fff;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
}

label {
    display: block;
    margin-bottom: 8px;
}

input[type="text"],
input[type="email"],
input[type="password"] {
    width: 100%;
    padding: 8px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

input[type="submit"] {
    background-color: #28a745;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 4px;
    cursor: pointer;
}

input[type="submit"]:hover {
    background-color: #218838;
}
```

### Step 6: Set Up the Server with Node.js and Express
Create `app.js` in the project root directory:
```javascript
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const app = express();

// Connect to MongoDB
mongoose.connect('mongodb://localhost:27017/registrationDB', { useNewUrlParser: true, useUnifiedTopology: true });

// Define User schema and model
const userSchema = new mongoose.Schema({
    name: String,
    email: String,
    password: String
});
const User = mongoose.model('User', userSchema);

// Middleware
app.use(bodyParser.urlencoded({ extended: true }));
app.use(express.static('public'));
app.set('view engine', 'ejs');

// Routes
app.get('/', (req, res) => {
    res.render('index');
});

app.get('/register', (req, res) => {
    res.render('register');
});

app.post('/register', (req, res) => {
    const newUser = new User({
        name: req.body.name,
        email: req.body.email,
        password: req.body.password
    });

    newUser.save((err) => {
        if (err) {
            res.send(err);
        } else {
            res.send('Successfully registered!');
        }
    });
});

// Start the server
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});
```

### Step 7: Create the Home Page
Create `index.ejs` in the `views` directory:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Home</title>
</head>
<body>
    <h1>Welcome to the Home Page</h1>
    <a href="/register">Register Here</a>
</body>
</html>
```

### Step 8: Run the Application
1. Start your MongoDB server (e.g., `mongod`).
2. Run your application:
    ```bash
    node app.js
    ```
3. Open your browser and navigate to `http://localhost:3000/register` to view the registration form.

You have now created a registration form with HTML, CSS, Node.js, and MongoDB, and uploaded your code to GitHub.
