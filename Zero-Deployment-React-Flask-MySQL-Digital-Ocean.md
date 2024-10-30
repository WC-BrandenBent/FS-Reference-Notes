# Full-Stack Application Development Guide

This guide should serve as a reference for how to set up a full stack application using the tools we have used in class. Do note that this is not the only way to create a full stack application, and if you have successfully created something without following these exact steps that does not mean you have done anything wrong. This is simply a reference for a single way to do things that I've organized in a way that I find makes the most sense. If you prefer to do things another way -_that works_-,then feel free to use this document as a reference/reminder for basic command-line commands that you may have forgotten

## Table of Contents

- [Full-Stack Application Development Guide](#full-stack-application-development-guide)
  - [Table of Contents](#table-of-contents)
    - [1. Project Initialization](#1-project-initialization)
      - [Note: Chaining commands in the terminal](#note-chaining-commands-in-the-terminal)
      - [Initializing a Git Repository](#initializing-a-git-repository)
      - [Connecting to a GitHub Repository](#connecting-to-a-github-repository)
    - [2. Backend Project Setup (Python \& Flask)](#2-backend-project-setup-python--flask) - [Setting Up Flask](#setting-up-flask) - [Folder and File Structure for Flask App](#folder-and-file-structure-for-flask-app)
    <!-- - [](#) -->
    - [3. Frontend Development (React \& Vite)](#3-frontend-development-react--vite)
      - [Setting Up React Project with Vite](#setting-up-react-project-with-vite)
      - [Folder Structure for Frontend](#folder-structure-for-frontend)
      - [Integrating Frontend with Backend API](#integrating-frontend-with-backend-api)
    - [4. Database Setup (MySQL)](#4-database-setup-mysql)
      - [Database Configuration](#database-configuration)
      - [Creating Tables and Relationships](#creating-tables-and-relationships)
    - [5. Testing the Application](#5-testing-the-application)
      - [Testing Backend Endpoints](#testing-backend-endpoints)
      - [Testing Frontend Functionality](#testing-frontend-functionality)
    - [6. Deployment](#6-deployment)
      - [Setting Up DigitalOcean Server](#setting-up-digitalocean-server)
      - [Configuring Environment Variables](#configuring-environment-variables)
      - [Deploying Backend and Frontend](#deploying-backend-and-frontend)
      - [Final Testing on Production](#final-testing-on-production)

---

### 1. Project Initialization

```bash
# Create a directory for your project
mkdir <YOUR-PROJECT-NAME>
# Enter the new empty directory
cd <YOUR-PROJECT-NAME>

```

###### Note: Chaining commands in the terminal

```bash
# You can chain commands in the command line to do multiple commands one-after-the-other.
mkdir <YOUR-PROJECT-NAME> && cd <YOUR-PROJECT-NAME>
# For the purposes of this document I will be splitting them apart for more easy reference, but below is an example of such a command for creating a directory and immediately entering it
```

#### Initializing a Git Repository

```bash
# Initialize Git repository locally on your machine
git init
```

#### Connecting to a GitHub Repository

1. Create a new repository on GitHub.
2. Connect your local project to the GitHub repository.

````bash
# Add remote origin, in other words "link" your local git repo with a remote repo hosted in some Git hosting service (Github in our case)
git remote add origin <YOUR_GITHUB_REPO_URL>

# Perform an initial commit and push to GitHub

# The "add" command stages all changes in the current directory so that they will be included in the next commit. The "." means "everything in this directory and all sub-directories". Combined they will stage all changes you have made
git add .
# The "commit" command saves all staged changes to the local Git history. the "-m" flag allows for a string to be included that will describe your changes, allowing for you and your team to keep track of what each commit is doing
git commit -m "Initial commit"
# The "push" command sends local commits somewhere. "origin" refers to to a specific remote repository. By default origin points to the repo URL from wherever you cloned from OR linked to with ```git remote add origin <URL>```. The "-u" flag stands for "upstream" and sets remote branch as the default remote branch for the current branch (in this case main). After this is set you will only have to type "git pull" or "git push" because git will "know" what remote branch you are referring to from now on
git push -u origin main
````

Note: You may run into an error when attempting to push if you don't have anything to add to the remote repo yet. Now is a perfect time to add a README.md and .gitignore file to the root of your project, if you didn't automatically generate them when creating your remote repo on Github

<!-- #### Creating Project Structure -->
<!---->
<!-- Use the command line to create the necessary folders for a structured project. -->
<!---->
<!-- ```bash -->
<!---->
<!-- # Create folders for backend, frontend, and configuration -->
<!---->
<!-- mkdir backend frontend -->
<!-- ``` -->

---

### 2. Backend Project Setup (Python & Flask)

#### Setting Up Flask

1. Create a virtual environment **and activate it**.

   ```bash
   # python3 (or simply python if your machine does not have any version of python older than python 3.0) performs a python action. The "-m" flag tells python to run a "module" -or file containing python definitions and statements- as a script. The first "venv" is the name of the module we are running, the second "venv" is the name we are giving our virtual environment. The second venv could be replaced with any valid file name, but typically you will them labelled venv or .venv
   python3 -m venv venv

   # source is a Unix command that can run a script in the current terminal session and will apply whatever changes are made to the terminal environment. venv/bin/activate is the path from our current directory to the script that the prevoius command created for us that activates the environment
   source venv/bin/activate
   ```

2. Install Flask and necessary packages.
   ```bash
   # pip is our package manager for our various python dependencies, any version of python past version 3.4 will come with pip automatically upon install
   pip install Flask flask-cors flask-sqlalchemy
   ```
   You likely will need more packages than these, this is just a short and simple reference document and is not created with the intent of being a full guide

#### Folder and File Structure for Flask App

This is the bare minimum you will need to seperate your python code. Do note that the "server" folder I am created will exist in the root (top level) of the project directory. See [Full Project Structure Example](#full-project-structure-example) for reference

```plaintext
server/
│
└── app.py # Main application entry point
```

Below is an example of how to create a directory and file via the command line, however there is nothing wrong with doing so via VSCode or your preferred editor/file manager

```bash
# Create a folder for our backend code. This can be named anything, but I will call it "server"
mkdir server
# Navigate into the new folder
cd server
# "touch" creates a new file and names it whatever you typed after the touch command
touch app.py
```

#### Activating Backend Server

After you have created a basic flask app and route you can run the command below to start your flask server (for testing that you've set everything up properly, I always make a simple route that prints "Hello World" when pinged)

```bash
# "--app" will indicate the name of the app we indend to run -in this case our file is named app.py, so the app's name is "app" without the extension. "run" will start the built in dev server, while the "--debug" flag will output helpful information in the terminal regarding the server
flask --app app run --debug
```

Double check that you are in the server directory if you are not able to start your server

<!---->
<!-- #### Creating RESTful API Endpoints -->
<!---->
<!-- #### Connecting to MySQL Database -->
<!---->
<!-- Guide on configuring a MySQL database and connecting it to Flask using \`SQLAlchemy\`. -->

### 3. Frontend Development (React & Vite)

#### Setting Up React Project with Vite

1. Use Vite to create a new React project. You can use other build tools, but Vite is currently very popular, reliable, and fast

   ```bash
   # npm is the node package manager and manages javascript packages. "init" initializes a project using the tool named afterward (in this case "vite") the final word "client" is what I am naming the folder that will be generated for me
   npm init vite client
   ```

   You will be asked what frameworks and languages you want vite to install the dependencies for automatically after running the command

2. Navigate to the \`client\` folder, install the required dependencies, and run the development server
   ```bash
   cd client
   # will install all dependencies, defined in the package.json
   npm install
   # will start the server in development mode
   npm run dev
   ```

#### Folder Structure for Frontend

Example structure:

```plaintext
client/
│
├── node_modules # stores JS dependencies
├── public/ # Used for static assets
├── src/
│ ├── components/ # This folder isn't created automatically, I make this to keep my project organized
│ ├── App.jsx # Main app component
│ └── index.jsx # Entry point
├── package.json # List of our dependencies required for our project with specific version numbers
└── vite.config.js # Vite configuration file
```

#### Integrating Frontend with Backend API

At this point you should be able to make a call from your front end to your backend to confirm everything is setup properly

---

### 4. Database Setup (MySQL)

#### Database Configuration

To Be Added

#### Creating Tables and Relationships

To Be Added

---

### 5. Testing the Application

#### Testing Backend Endpoints

Use a tool such as Postman to make sure each of your endpoints are functional to save time

#### Testing Frontend Functionality

To Be Added

---

### 6. Deployment

**_Note: If you are deploying on DigitalOcean, follow these steps. Please ensure you have an account set up and SSH access._**

To prepare for deployment we need to change a few things in our code depending on the method of deployment. This can be automated, but for the sake having a more thorough reference I will provide steps without any abstractions

#### Preparing Our Backend For Deployment

You'll notice when running `flask --app app run --debug` you get a warning that says `WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.` The development server we use is fast, but is lacking certain security features and is not optimized to handle many requests from many different users (which is never an issue during development, but we would like our apps to be used by more than us, so we need to change the server we use)

In our server directory we will install a tool called `Gunicorn` which is a stable and popular Python Web Server Gateway Interface HTTP server or WSGI

1. In our server directory install the python package

   ```bash
   pip install gunicorn
   ```

2. The command to run this server is:
   ```bash
   gunicorn --bind <ip_address>:<port> <name_of_flask_app>:<name_of_python_app_file>
   ```
   but we will be setting up the command inside whatever server/hosting-platform we use so it's not important yet

#### Preparing Our Frontend for Deployment

There are multiple ways to go about this, including allowing DigitalOcean to perform certain steps for us. Again, for reference I'll show the individual steps without any abstraction or magic

1. First we should build our React App, doing so will run a script that will read our code and create a new folder called `dist` which will contain any assets we require and optimizes our React code as much as possible beyond what we could do ourselves.
   - Examples of what's happening when we build:
     - `dist` folder will not have any .jsx files even though we wrote all our components in JSX. JSX is not valid Javascript, so browsers can't actually understand how to read it, what would normally happen is the JSX would be
     - Minification is performed on the JS (file sizes are reduced by automatically removing anything that a machine doesn't care about, such as comments, whitespace, and variable names are shortened automatically)
     - Files are combined into as few files as possible
     - Unused code that can be identified is removed (This is called Tree Shaking)
     - Environment Variables are injected into the code so that to the browser they appear "hard coded"
   - **Reminder:** building also created a single index.html, allowing us to deploy this single static file instead of an entire directory full of dozens and dozens of various "React" files
2. Make sure that you've performed an `npm install` and `npm build` before merging any changes to your main, as the `package.json` and `dist` folder contents will not update, meaning your static server holding your frontend will not update
3. If you've set up automatic redeployment, simply merge/push to the main branch and your server will rebuild. If you have not chosen to automatically redeploy upon main update, then you need to make sure that your chosen deployment process handles building and starting whatever server you are using

#### Setting Up DigitalOcean Server

DigitalOcean provides multiple ways to deploy your application, the main being their App Management Platform which will automate certain portions of the process, and their Droplets feature which are basically linux servers that can be accessed to download any tools, dependencies, etc to deploy your app. Below are the steps for using their App Management tool which integrates with your Github account to allow for automatic re-deployment whenever the main branch of your repo is updated

#### Deploying Backend and Frontend

1. Select the App Platform in the side bar and choose "Github" as your Service Provider. You can select the repository of your project (even if it is private!) if your Github account permissions are setup with your DigitalOcean account. If you do not see your repo, there is a link to update your permissions

2. Select the main Branch as the branch you want DigitalOcean to "watch" and update from when updated. You can leave the Source Directory as is, because it automatically will point to the root of your repo, which is typically want we want

3. In the `Source Directory` field you will have to set the path from the root of your Github Repo to your individual servers. Starting with the backend would mean you would type something like `/server`

4. DigitalOcean will determine what type of application and server you require depending on what it sees in the repo, but you can choose to edit the automcatic choices to choose a cheaper (and slower) server or to view what the cost of other choices.

5. You can add an additional resource by clicking the optional button to do so, choosing `Detect From Source Code` for static pages or web services, or simply choosing `Database` for databases, and you will be brought to the previous page. After selecting the same repo (assuming you are working with a mono-repo), you will path to the static file that was created from our building process of our react application, based off my naming standards mine is typically `/client/dist`

6. After your frontend and backend are included, you will want to go and add commands in each container to customize what happens when the server runs for the first time (and each subsequent time that the main branch is updated and your application is redeployed)

   - In the `Run Commands` of our flask server, we need to feed a command that will run our new production-ready server with gunicorn.

   ```bash
   # `--bind` will tell the gunicorn server to listen to all interfaces on a specified port on the machine it is serving from. `$PORT` is a special environment variable that DigitalOcean, we don't need to know what the port is as long as we set our server to listen to the variable where that number is saved. `app:app` informs the server of our Flask app and python application name to serve, it's a common practice to name both app
   gunicorn --bind 0.0.0.0:$PORT app:app
   ```

7. Configuring Environment Variables if necessary, the modern day tooling Digital Ocean (and many other platforms) provide make this very intuitive, simply follow the steps after you've set up your front and backend

8. Review all settings carefully, as well as the pricing (As of right now the slowest servers are only $5 monthly, while hosting static files is free up to a certain number per account with Digital Ocean)

#### Final Testing on Production

#### Quick Comparison of Popular Hosting Platforms

| Platform     | Best Suited For                                      | Ease of Use | Scalability | Customizability | Cost    |
| ------------ | ---------------------------------------------------- | ----------- | ----------- | --------------- | ------- |
| DigitalOcean | Small to medium-sized apps needing managed services  | Medium      | High        | Moderate        | $$      |
| AWS          | Enterprise-grade, complex applications               | Low         | Very High   | Very High       | $$$     |
| Heroku       | Prototypes, small-medium apps, fast deployments      | High        | Medium      | Low             | $$      |
| Vercel       | Front-end, static sites, serverless apps             | Very High   | High        | Low             | Free-$$ |
| Google Cloud | Data-intensive and globally distributed applications | Medium-Low  | Very High   | Very High       | $$$     |
