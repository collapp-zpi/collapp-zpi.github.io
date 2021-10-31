# Folder structure

### This project follows a specific folder structure. If you diverge from this set path, things might not work :sob: <!-- {docsify-ignore} -->

## components

<p align="center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4a/Font_Awesome_5_brands_react.svg/1200px-Font_Awesome_5_brands_react.svg.png" width="192" height="192">
</p>

This folder should contain all your **React** components. You might use or create as many component as needed but remember to have one component as a resulting plugin inside `client.jsx` file. Also if you need to wrap your plugin in **providers**, then that's the place to do that

It's important to leave this component named as `Plugin` and have it as a _default export_. You always get a prop called **websocket** that's an instance of websocket connection with the rest of the webapp.

<!-- tabs:start -->

#### **functional**

```jsx
import React from "react";

export default function Plugin(props) {
  return <div></div>;
}
```

#### **lambda**

```jsx
import React from "react";

const Plugin = (props) => {
  return <div></div>;
};

export default Plugin;
```

#### **class**

```jsx
import React from "react";

export default class Plugin extends React.Component {
  state = {};
  render() {
    return <div></div>;
  }
}
```

<!-- tabs:end -->

?> _client.jsx_ is your entry point to the system, as a prop your get a websocket instance passed to enable communication between plugin and the webapp

## logic

<p align="center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/99/Unofficial_JavaScript_logo_2.svg/1024px-Unofficial_JavaScript_logo_2.svg.png" width="192" height="192">
</p>

This folder should containt all your `javascript` logic that is used in the plugin. All these used scripts will be bundled by **webpack** with main component to create your plugin.

Logic is optional, especially with simple widgets. Except `server.js` file that containt declarations of operations on user data. That file is loaded on a server and invoked by your plugin. That way data operations are performed on a server, not client.

<!-- tabs:start -->

#### **base**

```javascript
const set = ({ broadcast }, input) => {
  broadcast("state", input);
  return input;
};

const open = ({ send, state }) => {
  send("state", state);
};

const events = {
  set,
  __OPEN: open,
};

export default events;
```

#### **example todo**

```jsx
const toggle = ({ broadcast, state }, index) => {
  const list = [
    ...state.slice(0, index),
    {
      ...state[index],
      isDone: !state[index].isDone,
    },
    ...state.slice(index + 1),
  ];
  broadcast("state", list);
  return list;
};

const add = ({ broadcast, state }, input) => {
  const list = [
    ...state,
    {
      text: input,
      isDone: false,
      timestamp: new Date().getTime(),
    },
  ];
  broadcast("state", list);
  return list;
};

const remove = ({ broadcast, state }, index) => {
  const list = [...state.slice(0, index), ...state.slice(index + 1)];
  broadcast("state", list);
  return list;
};

const open = ({ send, state }) => {
  send("state", state);
};

const events = {
  toggle,
  add,
  remove,
  __OPEN: open,
};

export default events;
```

<!-- tabs:end -->

Your plugin can store data regarding users in our database. Each instance of a plugin inside a user space gets a record in a databse, containing empty javascript object `{}`. Use that to store important data that must be preserved between sessions. A example of a stored data record regarding a todo list:

```javascript
{
  todos: [
    {
      done: false,
      content: "Get some milk",
    },
    {
      done: true,
      content: "Infiltrate foreign government",
    },
  ],
  description: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. In non orci vitae risus sodales ornare a in nisi."
}
```

## resources

<p align="center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/3/3f/Placeholder_view_vector.svg" width="254" height="254">
</p>

You can keep all resources you need inside resource folder. This folder will be bundled with the rest via **webpack**, hosted on a **S3 bucket** and statically delivered to users.

Resources might be images, text files, data files like json, excel or other, sound files, fonts, video formats, icons or any other format that might be served statically.

We would strongly advice to host your resources on your own hosting solutions to increase security, but if need be, keep it in `resources` folder

## styles

<p align="center">
    <img src="https://cdn.icon-icons.com/icons2/2699/PNG/512/tailwindcss_logo_icon_167923.png" width="254" height="254">
</p>

This folder should encapsulate all your style files. At your service you have quite a few ways to style your **HTML**

1. Our favourite - **TailwindCSS**
2. Plain **CSS**
3. CSS preprocessor - **SCSS**
4. **Module css**
5. If you wish to install - **Styled Components**

Keep your styles oranized inside `style` folder. PostCSS will minimalize outputed styles for production.
With `tailwind` you have a config file to customize your styles

```javascript
const colors = require("tailwindcss/colors");

module.exports = {
  mode: "jit",
  purge: [
    "./src/*.{js,ts,jsx,tsx}",
    "./src/core/*.{js,ts,jsx,tsx}",
    "./src/plugin/components/*.{js,ts,jsx,tsx}",
  ],
  darkMode: false,
  theme: {
    colors: {
      transparent: "transparent",
      ...colors,
    },
    screens: {
      xsm: "360px",
      sm: "640px",
      md: "768px",
      lg: "1024px",
      xl: "1280px",
      xxl: "1920px",
      xxxl: "2560px",
    },
  },
  variants: {
    extend: {},
  },
  plugins: [require("tailwindcss-textshadow")],
};
```

```javascript
PostCSS config
module.exports = {
  style: {
    postcss: {
      plugins: [require("tailwindcss"), require("autoprefixer")],
    },
  },
};
```

## config.json

<p align="center">
    <img src="https://www.svgrepo.com/show/1897/settings.svg" width="192" height="192">
</p>

This file contains some necessary configuration to your plugin. For a pack to be completed, required properties must be filled in.

```javascript
{
    "app_name": "someName",
    "default_size": {
        "width": 3,
        "height": 2
    }
}
```

## .env

```bash
SOME_VARIABLE="some value"
SECRET_KEY="big secret"
```
