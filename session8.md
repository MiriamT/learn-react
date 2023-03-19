# Session 8: Publishing to Github Pages

## Objectives

- What is Github Pages?
- Publishing a React app to Github Pages
- Assignment: Publish your demo site to Github Pages

## What is Github Pages?

[Github Pages](https://pages.github.com/) is a Github feature that enables you to host websites from your Github repositories. Github serves all of your project sites from a personal url tied to your username. The website content is pushed to a special Github Pages branch in your repo, usually named `gh-pages`, and Github serves that content when users access the Github Pages url for the repo.

Github Pages has 2 kinds of websites: a `User site` and a `Project site`. Each Github user only gets 1 User site, hosted at the root of their Github pages url (for example: `https://myusername.github.io`). Project sites are tied to repositories, and you can have 1 per repo (for example: `https://myusername.github.io/my-repo`). The project sites are hosted at urls nested under your main Github User site, but you don't need a User site to create Project sites.

## Publishing a React app to Github Pages

React apps built with Create React App are easy to integrate with Github Pages, using the following [guide](https://create-react-app.dev/docs/deployment/#github-pages). You'll install the `gh-pages` dependency, make a few modifications in your `package.json` file to tell Github how to configure your site, and then run `npm run deploy` to create your new Github Pages site.

When you want to update the content of your Github Pages site, usually after making updates to your React code, you'll run `npm run deploy` again. Make sure your site runs locally with no errors before running deploy, or you'll break your Github Pages site.

## Assignment: Publish your demo site to Github Pages

Follow the Guide above to deploy your Demo Site app to Github Pages.

The Demo Site is currently using `BrowserRouter` for page navigation, [which is not supported on Github Pages](https://create-react-app.dev/docs/deployment/#notes-on-client-side-routing). An easy fix for the Demo Site app is to replace `BrowserRouter` with `HashRouter`, which is also exported from `'react-router-dom'`. HashRouter will add a hash (`#`) into the url which becomes the base for relative page routing.

Here is an example Demo Site hosted on Github Pages: https://miriamt.github.io/learn-react-demo-app/
