## MASTER-TEMPLATE- (without auth) -Angular-Node.js-MongoDB by Jack Amsterdam in Typescript for a Full Stack Project **&copy;**
# This is mainly a template that I made to start a new Full Stack project using the MEAN stack.

![This is an image](Frontend/src/assets/images/mean-stack.png)

**If you are interested in a template with React and MySQL (with Authentication and Authorization in Node.js and React) please see my other templates.


## ___________________ Frontend/Backend Project by Jack Amsterdam in TYPESCRIPT **&copy;**


## If you used my template and enjoyed it (or had any issues), please contact me on Linkedin: **https://www.linkedin.com/in/jack-amsterdam/**

Backend detailed information only:

*__________________ is expanding its services online and I was asked to build a REST API for the backend with Node.js for ____________. I then built the rest according to Node's Layered Architecture. This REST allows you to get all of _______________ as well as add a ___________. Code is production ready.*

First of all the server is deployed on Heroku - **Go To -** [https://________-backend-____.herokuapp.com/api/](https://_________) **to see ______________.**

Secondly, I uploaded the server as a package to NPM that can run while you get________ and add _________. Can be downloaded here as a global package installation:

[https://www.npmjs.com/package/__________-backend-for-_____-by-jack-in-javascript](https://www.npmjs.com/package_______). Further instructions on how to run in README.MD

# Instructions to run the code on your local machine:

<!--```bash -->
<!-- ```Javascript -->

```
1. Git clone the repository.
2. There is a folder called Database -import the sql file into your phpMyAdmin or your MySQL Workbench.
3. Open terminal by clicking on the Backend folder and type: npm i && npm start.
4. Open a second seperate terminal by clicking on the Frontend folder and type: npm i && npm start.
5. Backend Server will run on http://localhost:3001
6. Frontend Server will run on http://localhost:4200
```
<!--5. Backend Server will run for you on [http://localhost:3001](http://localhost:3001)
6. Frontend Server will run for you on [http://localhost:4200](http://localhost:4200) -->

 *Possible errors - You did not open two seperate terminals and you are not running both servers or you did not upload the database properly.

### *Summary of stages I took in building this project:*

I made a Database in mySQL called _________ and I added a Table called ________. I then inserted  a couple of _______. Each ______ has an auto incremented ______ id , price, date, name, phone........ "edit"

I exported the database and put the file in the Database folder. To run the program in phpMyAdmin you need to import the file from this folder in the import tab in phpMyAdmin (after you ran Apache and mySQL on port 3306 using XAMPP).

###### In my Backend folder where node is I have the following Directory Structure dividing my files by Node's Layered Architecture מודל השכבות -

1. Utils folder -  with a config file - where all my configurations go, so If I want to change anything in the future I only need to apply the changes here. I also have a file called log-helper which uses Winston library to log requests in the format I specified and I display all requests and errors in logger.log file for informative logging.
2. Middleware folder - with the following middleware's  - an error handler to catch all errors thrown from any layer ( a catch all for all errors), I have a log-requests file which is middleware that logs every request to the logger.log file. I also have a sanitize file to prevent xss attacks so users can't for example send me a string with a script tag - it  will strip the tags.
3. Model folder - this is how the data is coming and represented from the mySQL database ____________.

I built an _____Model and an _______Model. So I am extending  the Base class _____Model with  _______Model to support ______s that are ______ for __________. I also have an ErrorModel class for error handling. These classes are used because I do not want to work with object literals. These objects are repeating themselves multiple times in my code so I made a class and then I made instances of a class. For example with the ErrorModel I have a status and message  and this saves me from making mistakes e.g. writing statussss instead of status. Additionally I am turning the request.body which is a literal object into an instance of an _______Model class so now that request.body has all the methods of that class (has all Joi validation methods for example). This makes my program more object oriented.

# **Layers:**

So, one of layered architecture's goals is to separate concerns among components. Another goal is to organize layers so they can perform a specific role within the app. I have the data access layer connecting to the database, business logic layer for all the logic and a controller layer with routes returning a response from the server.

Throughout the layers in each step I am returning a promise using async await syntax because it takes time for data to come back from the database and javascript is single threaded so I do not want to hog the call stack with each request.

4. Data access Layer folder - contains  a dal file that connects to the database. Since node's original functions in 2009  did not work with promises but with callbacks I had to  promisify the execute function. So the function returns a promise. I added a "values" parameter in order to prevent sql injections so characters will be escaped. Notice that my connection is using the config file so If you want to connect to a different database all you need is to change is the config file.
5. Business Logic Layer folder - contains _________ logic file that gets All the ______ by ______ and returns a promise and also adds a new _______ and returns a promise.
6. Controller Layer folder - contains orders controller - using express.Router() to have the routes here instead of in app.js. Contains_______"Enter number of Routes"____ routes that frontend can surf too.

app.ts - Instead of having all the above in app.ts I separated everything into layers. Here we start a server and  listen on port 3001 for connections as defined in my **.env** file which holds my environment variables.

# **Security**

I am using cors package so Angular frontend project, which usually runs on http://localhost:4200, won't have a cross origin issue.

I am using expressRateLimit package to prevent DOS attacks and limiting to 10  clicks per second and if you exceed you get an HTTP error  code and message: 429 (Too Many Requests).

I am using sanitize middleware to prevent xss attacks. As well as log requests middleware to log all requests and errors to a logger.log file using the winston library for informative logging.

If path is not found than my server.use(*) middleware will throw a HTTP error code of  404 Route not found error.

At the end of the app.js file you can see the errors-handler middleware to catch all errors that came from all layers. (Throwing errors in business logic and using next(err) to pass error to the err middleware).

You can see that all request and all errors are caught and displayed in logger.log using winston library.

For example in logger.log file the errors are displayed like this (because of my log-helper and log-request files which this middleware was added in app.js):

info    2022-09-18 01:01:46 GET Request to /api/_______________/  (Good route)

info    2022-09-18 01:02:07 GET Request to /api/productssss  (Bad Route)

info    2022-09-18 01:02:07 Route not found   (Error Message)

# **TESTING**

Import  *"__________________.postman_collection.json"*   to Postman and test the REST API there.  ( added edge cases of possible errors (400 Bad Request  and 404 Route not found)) All errors end up in errors-handler middleware.

Another option - Need to download *"REST Client"* extension in VSCode and you can check the server with the  restCLientExt.http file I provided.

# **EDGE CASES:**

If there are no _________ in the_________ I return 200 with a message - 'No ________ in the _______.

I added Joi validation when adding a new __________:

תקינות קלט:

-Forbidden to add new ID - because POST with REST  adds a new Id from the database ( According to REST Architecture you are not supposed to send ID with POST)

-All fields are required besides ______Id

-Price must be a number up to 100,000  "edit"

-Date must be a date greater than today________"edit"

-Name must be a string with max 30 characters   "edit"

-Address must be a string with max 100 characters  "edit"

-Phone must be a string with max 15 characters (using varchar (not int) in mysql -because of 0.)  "edit"

# Please check out my info:

https://www.linkedin.com/in/jack-amsterdam/

https://github.com/jackamsterdam

https://wakatime.com/@jackamsterdam

https://www.npmjs.com/~jackamsterdam

😃 THANKS FOR READING, AND HAVE A HAPPY DAY 😃
