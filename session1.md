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

### 2. Install ZSH and the [Oh My ZSH](https://ohmyz.sh/) terminal (optional)

- On [Mac](https://github.com/ohmyzsh/ohmyzsh/wiki)
- On [Windows](https://dev.to/vsalbuq/how-to-install-oh-my-zsh-on-windows-10-home-edition-49g2)

Note: ZSH is Linux-based and does not run perfectly on Windows. It generally offers a better developer experience, but you may need to run certain commands from CMD or Powershell.

### 3. Install [NodeJS v16 ](https://nodejs.org/en/)

Note: you might have done this as part of installing ZSH.

Check that you have the correct version installed:

```
> node -v
```

It should print `v16.x.x`.

### 4. Install [Git](https://git-scm.com/downloads)

Note: you might have done this as part of installing ZSH.

Check that you have the correct version installed:

```
> git --version
```

It should print `v2.x.x`.

### 5. Install the [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) plugin for Chrome

Most web developers use Chrome, and most React developers use the React Devtools plugin. It will make your life easier.

## Create a new React application

Use [Create React App](https://create-react-app.dev/) to create a new React app called demo-app:

```
> npx create-react-app demo-app
> cd demo-app
> npm start
```

After installing the new app and running the start command, your new web application should open at `localhost:3000`.

## Check in the application to Github

### 1. Create a Github account

Create an account with [Github](https://github.com/) so you can store your projects online.

Then create a [personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) so you can authenticate from git on the command line.

### 2. Create a new repository

Follow this [guide](https://docs.github.com/en/get-started/quickstart/hello-world) to create a new repository:

- Name your repo `mcon-343-demo-site`
- Do NOT include a README file, make sure all boxes are unchecked

### 3. Check in your React app to the repo

Follow the commands Github shows on your new repo page. The commands are copied below with specific insutrctions for this course. Run them in your terminal at the root of the new react app:

```
> git init
> git add . // stage all new changes
> git commit -m "first commit"
> git branch -M main
> git remote add origin <copy-git-ref-from-your-repo-page>  // the git ref will be similar to `https://github.com/MiriamT/mcon-343-demo-site.git`
> git push -u origin main
```

Refresh your Github repo page and you should see the React app files saved to the repo. Now you are ready to start building your app!
