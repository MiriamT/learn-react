# Session 1: Let’s Git started

## Objectives

- Install web development software
- Create a new React application
- Check in the application to Github

## Install Web Development Software

### 1. Install [Visual Studio Code](https://code.visualstudio.com/)

Once installed, open the Visual Studio Code editor and add the following plugins:

- Prettier – Code formatter
- GitLens – Git supercharged

Follow this [guide](https://scottsauber.com/2017/06/10/prettier-format-on-save-never-worry-about-formatting-javascript-again/) to setup prettier formatting on save.

### 2. Install [NodeJS v18](https://nodejs.org/en/)

Note: you might have done this as part of installing ZSH.

Check that you have the correct version installed:

```
> node -v
```

It should print `v18.x.x`.

### 3. Install [Git](https://git-scm.com/downloads)

Note: you might have done this as part of installing ZSH.

Check that you have the correct version installed:

```
> git --version
```

It should print `v2.x.x`.

### 4. Install the [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) plugin for Chrome

This will make your life easier when debugging issues in your React app.

## Create a new React application

Use [Create React App](https://create-react-app.dev/) to create a new React app called react-demo-app:

```
> npx create-react-app react-demo-app
> cd react-demo-app
> npm start
```

After installing the new app and running the start command, your new web application should open at `localhost:3000`.

## Check in the application to Github

### 1. Create a Github account

Create an account with [Github](https://github.com/) so you can store your projects online.

Then create a [personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) so you can authenticate from git on the command line.

### 2. Create a new repository

Follow this [guide](https://docs.github.com/en/get-started/quickstart/hello-world) to create a new repository:

- Name your repo `react-demo-app`
- Do NOT include a README file, make sure all boxes are unchecked

![New Github repo](https://github.com/MiriamT/learn-react/blob/main/images/session1_new_repo.png?raw=true)

### 3. Check in your React app to the repo

Follow the commands Github shows on your new repo page for "push an existing repository from the command line".

Run the commands in your terminal at the root folder of the new react app (the same location where you ran "npm start" to start your web app):

![Push new repo](https://github.com/MiriamT/learn-react/blob/main/images/session1_push_repo.png?raw=true)

Refresh your Github repo page and you should see the React app files saved to the repo.

Now you are ready to start building your app!

> **Recommended:** New to Git? Learn the basic commands with this [interactive tutorial](https://learngitbranching.js.org/?locale=en_US).

![Saved repo](https://github.com/MiriamT/learn-react/blob/main/images/session1_github_repo.png?raw=true)
