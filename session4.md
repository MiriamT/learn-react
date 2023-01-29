# Session 4: Routes and Paths

## Objectives

- Learn the components of a URL
- Add React Router to render content based on the url path
- Assignment: Create an app header that links to each page

## Learn the components of a URL

A URL (Uniform Resource Locator) is made up of several segments: a scheme, a host / domain, a port (optional), a path (optional), and a query string (optional).

> **Assignment:** Read more about [URLs](https://www.ibm.com/docs/en/cics-ts/5.3?topic=concepts-components-url).

## Add React Router

Install React Router and add browser routes for the `<Home>` and `<Todo>` components by following the [React Router quick start tutorial](https://reactrouter.com/docs/en/v6/getting-started/overview).

Update the code in `App.js` to enable routing. `<Home>` should render at the base route (`/`) and `<Todo>` should render at `/todo`.

Test out your router by visiting the following urls:

- `localhost:3000` // should show your home page
- `localhost:3000/todo` // should show your todo page

## Assignment: Create an app header

Create a Header for your application that links to the different pages in your app.

Import Material UI's [`AppBar` component](https://mui.com/components/app-bar/). Show the name of your app (`'Demo'` or whatever name you choose) as well as a navigation item for `'Todo'`.

To connect your header links to the routes, bind React Router's [`useNavigate()` hook](https://reactrouter.com/docs/en/v6/api#usenavigate) to the `onClick` prop of the navigation items.

You should now be able to navigate back and forth between your home page and todo page by clicking on the navigation items in the header.

Uh oh! The todo app loses its data when you navigate back and forth from the the `/todo` page. Let's fix that in the next session by adding global state to the app.

![Session 4 Complete](https://github.com/MiriamT/learn-react/blob/main/images/session4_complete.png?raw=true)
