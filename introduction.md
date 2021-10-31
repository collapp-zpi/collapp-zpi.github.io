# Introduction

:computer: This section will be a introduction to when, where and why this project was made.

## Website overview

<p align="center">
    <img src="_media/icon.svg" height="192">
</p>

This documentation has been made to aid your attempts at plugin creation. Our website is called `Collapp`, a site that lets its users create workspaces to collaborate with others. Each workspace can be customized by adding relevant _plugins/extensions_, all written by the community!

> You can see out [website](https://collapp.live) live right now!

Potential plugin developers can create a `developer account`, allowing them to create, delete, update and overall manage their creations. A newly created developer account can be linked by `Github` account.
Regular users can log in with login/password credentials and admins have magic links send to them.

Plugins go through a **very meticulous verification** process before being allowed into the system.

## Why is it a thing?

<p align="center">
    <img src="_media/hat.svg" height="192">
</p>

### This project is a part of out **Engineer's Thesis**. <!-- {docsify-ignore} -->

It's sole purpose is to create a solid ground for deliberations and to showcase different technologies and methods used.

The biggest hurdle we decided to overtake in our theses was a remote execution of components at runtime and their secure render. Another aspect of our work regards user management and permissions as well as fast and reliable frontend delivery.

?> Our final is divided into three different thesis topics that we work on separately

## Ideas behind it all

## Technologies used

### Frontend

<p align="center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/8e/Nextjs-logo.svg/1280px-Nextjs-logo.svg.png" height="192">
</p>

As a rendering library at our site we use `React`.

Actually, it's a React component that fulfils the role of a plugin. Framework used on frontend is called `Next.js` and it is provided to us by `Vercel`. Since next.js work with many paradigms of rendering React pages, we are more flexible to choose how we want to render each page (we can render on client **CSR**, on the server **SSR** or in a hybrid manner **ISR**). Free hosting with global **CDN** of our frontend is also provided to us by `Vercel`

### Backend

<p align="center">
    <img src="https://seeklogo.com/images/N/nodejs-logo-D26404F360-seeklogo.com.png" height="192">
</p>

Because we use **Next.js** our backend managed to shrink considerably. For most simple endpoints we can use `serverless functions` provided by `Vercel`. That makes out technology stack very similar to ideas conjured by `JAMstack`.

```javascript
export default function handler(req, res) {
  res.status(200).json({
    body: req.body,
    query: req.query,
    cookies: req.cookies,
  });
}
```

For the rest of our services we use `Node.js` with `Express` framework. After all even serverless functions run on **node enviroment**. Backend is very loosely connected, divided into **microservices** and connected via messaging queues like `RabbitMQ`

### Database

<p align="center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/29/Postgresql_elephant.svg/1200px-Postgresql_elephant.svg.png" height="192">
</p>

To store all used data in our app we use **PostgreSQL** as it work very well with our **ORM** - `Prisma`.

Thanks to `Prisma` it's easy to retrieve and manipulate the data inside the database without the necessity to write raw SQL queries. It's also a tool to visualize data and perform migrations

### Styling

<p align="center">
    <img src="https://cdn.icon-icons.com/icons2/2699/PNG/512/tailwindcss_logo_icon_167923.png" height="256">
</p>

For our styling we decided to use `TailwindCSS` as a style manager and `Styled Components` to create reusable components.

Because Tailwind is so low-level, it never encourages you to design the same site twice. Even with the same color palette and sizing scale, it's easy to build the same component with a completely different look in the next project.

`Tailwind` automatically removes all unused CSS when building for production, which means your final CSS bundle is the smallest it could possibly be. In fact, most Tailwind projects ship less than 10kB of CSS to the client.

## Hopes and dreams

Lorem ipsum dolor sit amet, consectetur adipiscing elit. In laoreet, magna ut dictum luctus, libero ipsum rutrum mi, sit amet facilisis dui diam eu purus. Mauris mollis id ligula a bibendum. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin purus magna, cursus nec purus a, commodo dapibus nulla. Mauris et consectetur est. Nulla facilisi. In fermentum, risus at aliquam posuere, sapien sem pharetra purus, vel luctus nisl nisi et neque. Mauris sed tortor scelerisque, commodo neque finibus, condimentum elit.

Duis dignissim vitae purus ac convallis. Praesent aliquet vel enim in malesuada. Duis ac sapien et nisl congue dignissim. Aliquam auctor arcu non dui tempus, quis mattis leo egestas. Etiam lobortis at mi id molestie. Sed neque magna, accumsan nec aliquet eu, pharetra nec mi. Vestibulum vel congue leo, non aliquam sem. Donec pharetra, nisi in posuere vehicula, dui urna volutpat tellus, vel laoreet nulla felis eget diam. Nulla ultrices, leo id lobortis luctus, mauris metus eleifend diam, et interdum est ipsum non dolor. Quisque rutrum ullamcorper est, non imperdiet quam sodales dapibus. Maecenas convallis vel ex sit amet ultricies.

Lorem ipsum dolor sit amet, consectetur adipiscing elit. In laoreet, magna ut dictum luctus, libero ipsum rutrum mi, sit amet facilisis dui diam eu purus. Mauris mollis id ligula a bibendum. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin purus magna, cursus nec purus a, commodo dapibus nulla. Mauris et consectetur est. Nulla facilisi. In fermentum, risus at aliquam posuere, sapien sem pharetra purus, vel luctus nisl nisi et neque. Mauris sed tortor scelerisque, commodo neque finibus, condimentum elit.

Duis dignissim vitae purus ac convallis. Praesent aliquet vel enim in malesuada. Duis ac sapien et nisl congue dignissim. Aliquam auctor arcu non dui tempus, quis mattis leo egestas. Etiam lobortis at mi id molestie. Sed neque magna, accumsan nec aliquet eu, pharetra nec mi. Vestibulum vel congue leo, non aliquam sem. Donec pharetra, nisi in posuere vehicula, dui urna volutpat tellus, vel laoreet nulla felis eget diam. Nulla ultrices, leo id lobortis luctus, mauris metus eleifend diam, et interdum est ipsum non dolor. Quisque rutrum ullamcorper est, non imperdiet quam sodales dapibus. Maecenas convallis vel ex sit amet ultricies.
