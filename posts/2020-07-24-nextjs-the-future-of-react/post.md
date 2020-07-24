---
date: 2020-07-24
title: Next.js - the future of React?
published: true
description: A short overview of probably most versatile framework for React
tags: nextjs, react, javascript, typescript
cover_image: cover-next.png
---

React and Angular are probably the most popular, competing frameworks right now. They are being used in thousands of commercial and non-commercial projects around the globe. If you ever googled for differences between both of them, you would learn that despite React being a wonderful framework, it's not entirely ready out-of-the-box experience. Angular still has a couple of aces in sleeves. But with [Next.js],(https://nextjs.org/) React can overcame its shortcomings and perhaps end the old dispute "React vs Angular" in it's favour. 

# Why React is not complete

The quick answer: It was never designed to be a complete, big framework for all our developer needs. It started as just a view library - so just the V of the MVC approach. It quickly revolutionised web, gaining more popularity with new and fresh concepts like Flux, and then the Redux itself. More and more developers got excited about it and started releasing hundreds upon hundreds of middlewares and utilities to turn this primarily View framework into something more complete. Now, with its rich ecosystem of libraries, we can use it to create basically any app we can think of.

The problem is, that with all of the support from its community, it is tedious to start a new React project. Even with the usage of [Create React App](https://github.com/facebook/create-react-app), you still need to think about and integrate:
* state management, 
* middlewares to handle sideeffect if you happen to pick Redux,
* routing solution
* and many, many more...

It takes time and experience to set-up everything in an optimal way. No wonder that some developers prefer Angular. Once you install it, you're ready to start developing. Angular comes with a bunch of useful utils. Notably: Built-in router, state management, and basically convention-over-configuration approach. It just works.

We can't blame React for not having everything out-of-the-box, as it was never its intent. Luckly, there is Next.js to fill in the gaps and help us getting up and running in no time!

# Discovering Next.js

So what is Next.js? It is basically a framework for React. If you consider React to be a framework (I do!), then it's a framework for a framework. It tries to address the issues that I mentioned before and deliver a ready-to-go platform. We can just install it and we have (almost) everything we need to start our project. It doesn't matter if it's a passion project done after hours, or a commercial project for a big client. Next.js got us covered. Let's take a look at its features.

## Simple Setup

All we have to do in order to get a new app is simply typing the following in our terminal:

```
yarn create next-app
```

The creator will ask us two questions: Whats the name of your app and do you want to use a template. I suggest going with the default option for the latter one, although you can check existing templates if you're feeling adventurous. 

After everything is done, we end up with the following structure

```
node_modules/
pages/
  api/
    hello.js
  index.js
public/
  favicon.ico
  vercel.svg
.gitignore
package.json
README.md
yarn.lock
```

If we type the following, our app will start in development mode with hot reloading enabled! So cool! Type in the following to see your page live over `http://localhost:3000`:
```
yarn dev
```

Tip: I suggest moving the `pages/` folder into `src/pages/` so we can keep all of our source files into the `src` folder. Next.js will use `src/pages` as well.

## Routing

As mentioned before, Next.js has a pretty powerful routing included. What can be a bit inconvenient for newcomers is that it relies heavily on conventions rather than configuration. All JavaScript files placed in our `pages/` or `src/pages` will be mapped to an URL that user can access from the browser. `pages/index.js` will be accessible at the page root, `pages/users.js` can be seen at `mypage.com/users` etc... For deeper nesting you need to utilize directories, meaning that `pages/a/b/c.js` will turn into `mypage.com/a/b/c`. Simple as that.

Obviously, without support for dynamic arguments in URLs, we could not go very far. Fortunately, Next.js utilizes the file naming convention to help us with that. Simply, to handle `users/edit/{user-id}` URL, just create the file `pages/users/edit/[userId].js`. We can access the `userId` value by using the provided `useRouter` hook:

```javascript
import { useRouter } from 'next/router'

const Users  = () => {
  const router = useRouter()
  const userId = router.query.userId

  // rest of your logic
}

export default Users
```

## Linking

As a small bonus to the routing, Next.js comes with built in linking solution. Available in the `next/link` package, the component will help us link to our pages in more optimised way. 
```jsx
<Link href="/users/[userId]" as="/users/1">
  <a>See the first user</a>
</Link>
```

By using the provided `Link` in addition to the good old `a`, we can make use of enabled by default prefetching, making our pages load faster. Moreover, even when working in Server Side Rendered mode, the `Link` will allow us to actually render the page on the client side, making it kind of a smart SSR/SPA hybrid. 

There is a number of options for the `Link`, so we can very easily change its behaviour to use `history.replace` instead of calling `history.push` or just perform a shallow rendering (updating the URL without updating the page contents). 

## API support

This is where we dive into more advanced features. Next.js is more than purely Frontend framework. With it, we can develop also Backend endpoints very easily. 

Following the convention of routing, every file placed inside the `pages/api` directory will turn into an endpoint that we can call from the browser. The default file `api/hello.js` shows us how simple it is to create working endpoints returning JSON data:

```javascript
export default (req, res) => {
  res.statusCode = 200
  res.json({ name: 'John Doe' })
}
```

From here, nothing stops us from doing our backend logic, like querying a database. We need just to install our favourite ORM and we're ready to go.

## Server Side Rendering

This was one of the features that blown my mind. Next.js comes with an excellent support for SSR! I was actually in a project, where client decided, that they want to have SSR enabled. But we developed everything as client side rendered page. Luckly, Next.js was here to help us making the switch quite quckly.

As an example, let us consider this very simple, completely client rendered page:

```jsx
// pages/todo/[id].js
import React, { useState, useEffect } from 'react';
import { useRouter } from 'next/router'

const Todo = () => {
  const [data, setData] = useState(null);
  const router = useRouter()
  const id = router.query.id

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/todos/' + id)
      .then(response => response.json())
      .then(json => setData(json))
  }, [id])

  return <div>Todo - {data ? data.title : 'loading...'}</div>
}

export default Todo
```

In oder to convert it into a fully server side rendered page, we need only to export additional async function named `getStaticProps` and move our data fetching logic there. 

```jsx
// pages/todo/[id].js
import React from 'react';

const Todo = ({ data }) => {
  return <div>Todo - {data.title}</div>
}


export const getStaticProps = async (ctx) => {
  const id = ctx.params.id;
  const data = await fetch('https://jsonplaceholder.typicode.com/todos/' + id)
    .then(response => response.json());
    
  return {
    props: {
      data
    }
  }
}

export default Todo;
```
We have just turned our CSR page into a fully SSR page. That's incredible simple!

## Static Pages Generator

Sometimes we need just a simple, static pages generated with no need for node.js server. In a very similar manner to the SSR, Next.js allows us to quickly create statically generated pages. Let's consider the SSR example - we need only to export additional method called `getStaticPaths` that will tell Next.js what IDs are available. 

Obviously, if we're generating site based on DB or some CMS, we need to retrieve all of the valid IDs here. At the end, simply return the object with all IDs. The whole code for a statically generated page is as follows:

```jsx
// pages/todo/[id].js
import React from 'react';


const Todo = ({ data }) => {
  return <div>Todo - {data.title}</div>
}


export const getStaticProps = async (ctx) => {
  const id = ctx.params.id;

  const data = await fetch('https://jsonplaceholder.typicode.com/todos/' + id)
    .then(response => response.json());
  
  return {
    props: {
      data
    }
  }
}


export const getStaticPaths = async () => {
  return {
    paths: [
      { params: { id: '1' } },
      { params: { id: '2' } },
      { params: { id: '3' } }
    ],
    fallback: false
  };
}

export default Todo;
```

Once we have all of the pages prepared this way, we can simply call the `next build` and `next export` commands. Lo and behold, our static pages are generated! What I find even more impressive, is that almost all of our routing features (like prefetching) will work in static pages as well.

## TypeScript support

If you, just like me, prefer to have types in your project, then Next.js is perfect. Though it does not get generated as a TypeScript project, it can be easily converted to one. All we have to do is create an empty `tsconfig.json` file in the root directory and run our app. Next.js will fill the config with its initial configuration and will be ready to work with our TypeScript code. As simple as that!

Alas, There are small caveats. Firstly, it is better to not change the existing properties in `tsconfig.json`. For example, in one project I tried to disable the flag `skipLibCheck`, but that caused the compiler to rise an error in one of the Next.js dependencies. So I strongly advice not to change the existing config. Adding new properties is cool, though!

Secondly, the documentation is mostly written for good ol' JS. That means it might be sometimes problematic to find the type of a param for function. For instance, let's take a look again on the example from API support:

```javascript
export default (req, res) => {
  res.statusCode = 200
  res.json({ name: 'John Doe' })
}
```

We need to dig around in the docs, to figure out that the `req` object is actually of `NextApiRequest` type while `res` uses `NextApiResponse`. Not a deal breaker, but it's a bit annoying to look for the types.

## Downsides

Next.js, as everything in life, is definitely not perfect and has its own shortcomings. Have you noticed already that I haven't mentioned anything about state management? It's because Next.js, as packed with features as it is, does not provide us a built-in state manager. It is a kind of a bummer, that in all it's glory, with ready-to-go attitude, there is no state management. 

But I guess it makes sense. Lately state management in React apps became a bit of a controversial topic. There are a lot of people saying Redux is great (including me, but I also acknowledge its flaws). On the other side, there are people saying MobX is the way to go. Finally, there are devs who would argue, that Context API is all we need, or something exotic like `unstated-next` can be used (I don't recommend that one). With all those divisive opinions, it's no surprise that Next's devs haven't just picked one solution. Additionally, to be honest, with such a versatile tool, it would be probably hard to find an optimal solution. 

But if we really need a state manager in our app, there are a lot tutorials on the web showing how we can quickly add Redux or MobX.

Another (albeit small) downside of Next.js is lack of out-of-the-box support for any of CSS-in-JS technologies. We can use CSS and SCSS right from the get-go. But when it comes to more modern styling approaches, we need to add some code. It's not a lot, though, and there examples linked in the official docs ([here](https://nextjs.org/docs/basic-features/built-in-css-support#css-in-js)).

# Summary

As we can see, Next.js is a great and really versatile framework for React. It provides a well configured, working out-of-the-box environment for creating basically ANY web app. Basically, Next is perfect for Single Page Apps, Server Side Rendered pages, Statically Generated pages or anything in between. With API support we can use it to create a complete pages with Backend logic. The only really big downside, is that there is no built-in state manager. Apart from that, it's got everything we need to create new web apps in no time.

In conclusion, I believe it's the most complete React experience out there. Next.js provides all features that just pure React is lacking of, making it feature-ready setup to face Angular in the "React vs Angular" debate. If React is ever to win said dispute, it will need a solid framework to do so. In my opinion, Next.js is exactly that, an incredible environment for modern web app development.