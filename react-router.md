---
title: React Router Guide
description: React Router is a widely used library for managing routing in React applications. It allows developers to build single-page applications (SPAs) that use dynamic URLs to navigate between different pages without reloading the entire page.
published: true
date: 2023-06-03T00:00:00.000Z
---

React Router is a widely used library for managing routing in React applications. It allows developers to build single-page applications (SPAs) that use dynamic URLs to navigate between different pages without reloading the entire page. In this article, we will dive into the basics of React Router and explore some of its key features.

React router uses what we call <mark>client side routing</mark>, unlike the conventional approach when we build a website with html css and vanilla JS, a web browser initiates a request to a web server, receives and processes CSS and JavaScript assets, and renders the HTML content provided by the server. Each time a user clicks on a link, the entire process is repeated for the new page. This article will be broken in 4 sections.

1. What is React Router?

2. React Router Basics

3. React Router Advanced Features

4. React Router Best Practices

### What is React Router?

React Router is a library that provides a way to handle routing in React applications. It enables developers to define different routes for their application, each corresponding to a specific URL.

When a user navigates to a certain URL, the React Router library will render the appropriate component for that route. React Router also provides a number of features that make it easy to build complex routing scenarios. These include nested routes, dynamic routing, and programmatic navigation.

Assuming you have a React application set up using CRA (create react app ) or other React framewrok like Next js, you can install React Router using npm, yarn or any other package manager:

```bash
npm install  react-router-dom
```

or

```bash
yarn add  react-router-dom
```

### React Router Basics

React Router provides a number of components that you can use to define routes for your application. The easiest way to integrate React Router into
your application is to wrap you root component with the BrowserRouter component. This component will provide the routing context to all the components
in your application.

```jsx
import { BrowserRouter } from "react-router-dom"

const App = () => {
  return (
    <BrowserRouter>
      <div>
        <h1>My React App</h1>
      </div>
    </BrowserRouter>
  )
}
```

The router works just like context providers in React. It provides the routing context to all the children components.

### Defining Routes

Like we said earlier, React Router provides a number of components that you can use to define routes for your application. Now that we have wrapped our root component with the BrowserRouter component, we can start defining routes for our application.
To define routes, we will use 2 components provided by React Router: Route and Routes.
The Routes component is a wrapper for the Route components that you want to render in your application. It is used to group routes together and to provide a fallback component that will be rendered when no route matches the current URL.And the Route component that you use to render when a user navigates to a specific URL. The Route component takes a path prop that specifies the URL for the route. The component prop specifies the component that should be rendered when the user navigates to the specified path.

```jsx
import { Routes, Route } from "react-router-dom"

const App = () => {
  return (
    <div>
      <h1>My React App</h1>
      <Routes>
        <Route path="/todos" element={<Todos />} />
        <Route path="/users" element={<Users />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </div>
  )
}
```

In this example we have defined 2 routes for our application. The first route will be rendered when the user navigates to the /todos URL. The second route will be rendered when the user navigates to the /users URL. If the user navigates to any other URL, The last Route component will be executed it will render the NotFound component. The \* character is a wildcard that matches any URL that is not matched by the other routes that are defined above it.

One of the most important advantages of using the Route component is that it will only refresh the component that is rendered by the route. This means that the rest of the application will not be reloaded. This is a huge advantage over the traditional approach of building a website with HTML, CSS, and vanilla JavaScript.

### Implementing Navigation

To handle user navigation, React Router provides a Link component that you can use to create links to different routes. The Link component use the HTML anchor tag under the hood. It takes a to prop that specifies the URL for the link. When the user clicks on the link, the browser will navigate to the specified URL and the component that is rendered by the route will be refreshed.

```jsx
import { Link } from "react-router-dom"

const App = () => {
  return (
    <div>
      <h1>My React App</h1>
      <nav>
        <ul>
          <li>
            <Link to="/todos">Todos</Link>
          </li>
          <li>
            <Link to="/users">Users</Link>
          </li>
        </ul>
      </nav>
      <Routes>
        <Route path="/todos" element={<Todos />} />
        <Route path="/users" element={<Users />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </div>
  )
}
```

This is a basic example of how to use React Router to build a simple application. In the next section, we will explore some of the more advanced features to handle more complex routing scenarios.

#### Advanced Navigation Features

In this section, we will explore some of the more advanced features that React Router provides to handle more complex routing scenarios. We will go over these features in the following order:

1. Nested Routes
2. Dynamic Routes
3. Programmatic Navigation

### Nested Routes

Nested routes are routes that are defined inside another route. This is useful when you want to when you have components that contain other components. For example, you might have a component that renders a list of users. Each user in the list should have a link to a page that displays the details of the user. In this case, you can define a nested route for the user details page.

```jsx
import { Routes, Route } from "react-router-dom"

const App = () => {
  return (
    <div>
      <h1>My React App</h1>
      <Routes>
        <Route path="/users">
          <Route index element={<Users />} />
          <Route path=":userId" element={<UserDetails />} />
        </Route>
      </Routes>
    </div>
  )
}
```

In this example, we have defined a nested route for the user details page. The nested route is defined inside the Users component. The nested route will be rendered when the user navigates to the /users/:userId URL. The :userId part of the URL is the dynamic part of the URL. We will explore dynamic routes in the next section. As you can see, the code for the "/users" route changed now we have 2 Route components inside it. The first Route component is the index route. The index route is rendered when the user navigates to the /users URL. The second Route component is the nested route. The nested route is rendered when the user navigates to the /users/:userId URL.

We can't cover nested routes in React Router without mentioning the Outlet component. The Outlet component is used to render the nested routes. It will be rendered inside the parent component that contains the nested routes. The Outlet component will render the component that is rendered by the nested route.

```jsx
import { Outlet } from "react-router-dom"

const Post = () => {
  return (
    <div>
      <h2>Posts</h2>
      <Outlet />
    </div>
  )
}

const Comments = () => {
  return <div>Comments</div>
}

function App() {
  return (
    <div className="App">
      <Routes>
        <Route path="/post" element={<Posts />}>
          <Route path="comments" element={<Comments />} />
        </Route>
      </Routes>
    </div>
  )
}
```

In this example, we have defined a nested route for the comments page. The nested route is defined inside the Post component. The nested route will be rendered when the user navigates to the /posts/comments URL. So we will see in the browser something like this:

```html
<div class="App">
  <h2>Posts</h2>
  <div>Comments</div>
</div>
```

### Dynamic Routes

Dynamic routes are routes that contain dynamic segments. These segments are defined using the : character. For example, the /users/:userId route contains a dynamic segment that is defined using the :userId part of the URL. The value of the dynamic segment will be available in the match object that is passed to the component that is rendered by the route.

```jsx
import { Routes, Route } from "react-router-dom"
import { useParams } from "react-router-dom"

const UserDetails = () => {
  const { userId } = useParams()
  return <div>User Details for user {userId}</div>
}

const App = () => {
  return (
    <div>
      <h1>My React App</h1>
      <Routes>
        <Route path="/users">
          <Route index element={<Users />} />
          <Route path=":userId" element={<UserDetails />} />
        </Route>
      </Routes>
    </div>
  )
}
```

In this example, we have defined a dynamic route for the user details page. The dynamic route is defined inside the Users component. The dynamic route will be rendered when the user navigates to the /users/:userId URL. The :userId part of the URL is the dynamic part of the URL. The value of the dynamic segment will be available in the match object that is passed to the component that is rendered by the route. If the user navigates to the /users/123 URL, the UserDetails component will be rendered and the userId variable will be set to 123. The useParams hook is used to access the value of the dynamic segment in this case we are accessing the value of the userId for the URL.

### Programmatic Navigation

Programmatic navigation is the ability to navigate to a different route from within your application. This is useful when you want to navigate to a different route when a user performs an action. For example, you might want to navigate to the user details page when the user clicks on a user in the list of users.

```jsx
import { useNavigate, useParams } from "react-router-dom"

const UserDetails = () => {
  const navigate = useNavigate()
  const { userId } = useParams()
  return (
    <div>
      <div>User Details for user {userId}</div>
      <button onClick={() => navigate("/users")}>Go Back</button>
    </div>
  )
}

const App = () => {
  return (
    <div>
      <h1>My React App</h1>
      <Routes>
        <Route path="/users">
          <Route index element={<Users />} />
          <Route path=":userId" element={<UserDetails />} />
        </Route>
      </Routes>
    </div>
  )
}
```

React Router provides many hooks that you can use to access the current location, navigate to a different route, and more. The useNavigate hook is used to navigate to a different route from within your application. In this example, we are using the useNavigate hook to navigate to the /users URL when the user clicks on the Go Back button.
