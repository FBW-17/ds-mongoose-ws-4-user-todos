# Mongoose Workshop - Exercise #4 - User ToDos

Now we want to prevent that users can see each others todos!
A user must login to see his own ToDos.

## Task: Show user todos only

* Install package jsonwebtoken `npm i jsonwebtoken`

* Adapt your GET route /todos
    * Check for existence of a JWT token in req.headers.authorization
    * If token not present:
        * Show error message "No token present. Please login" together with status 401 (Unauthorized)
    * If token present:
        * verify token using jwt.verify(token, secret) method
        * store the result of jwt.verify in a variable
            * console.log the variable
            * in log you should see user data with the ID of the user
        * fetch todos JUST of this user!
            * hint: `ToDo.find({...}).then(todos => ...)`

* Adapt your POST route /login
    * Increase the expiry time to 5 hours (=> expiresIn: "5h")

* Testing - Use RESTED client (or fetch in Browser console)
    * Login a user (call POST /login with valid credentials)
        * Copy the received token
    * Call the GET route /todos in RESTED
        * Set a header "Authorization" with value of your token
    * Now you should get just the todos of the given user
    * Try once more to login as another user
        * Fetch the todos of that user

Congratulations. You now created your first multi-user application!


### Bonus Task - Check authorization header with validator

With express-validator we can not just validate body and params. We can also validate HTTP headers.

* Import the "header" function from the express-validator package
* Write a middleware that checkes for presence of the authorization header: `header('authorization').notEmpty()`
    * See also: [Express-Validator check sources](https://express-validator.github.io/docs/check-api.html)
* Call method validationResult() to get the errors
* If validationResult delivers errors: Send error message
