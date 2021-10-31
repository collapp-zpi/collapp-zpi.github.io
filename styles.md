# Styles and customization

We provide sereral ways for your plugin to be styles :fireworks:
<br />
Use your preferred method or mix and mash according to your needs.

?> We would highly recommend you use `tailwindCSS` as your styling library. Go on and read some more right here on the [official website](https://tailwindcss.com/)

## TailwindCSS

<p align="center">
    <img src="https://cdn.icon-icons.com/icons2/2699/PNG/512/tailwindcss_logo_icon_167923.png" height="316">
</p>

A utility-first CSS framework packed with classes like flex, pt-4, text-center and rotate-90 that can be composed to build any design, directly in your markup.
Utility classes help you work within the constraints of a system instead of littering your stylesheets with arbitrary values. They make it easy to be consistent with color choices, spacing, typography, shadows, and everything else that makes up a well-engineered design system.

Because Tailwind is so low-level, it never encourages you to design the same site twice. Even with the same color palette and sizing scale, it's easy to build the same component with a completely different look in the next project.

`Tailwind` automatically removes all unused CSS when building for production, which means your final CSS bundle is the smallest it could possibly be. In fact, most Tailwind projects ship less than 10kB of CSS to the client.

```jsx
<figure class="md:flex bg-gray-100 rounded-xl p-8 md:p-0">
  <img class="w-32 h-32 md:w-48 md:h-auto md:rounded-none rounded-full mx-auto" src="/sarah-dayan.jpg" alt="" width="384" height="512">
  <div class="pt-6 md:p-8 text-center md:text-left space-y-4">
    <blockquote>
      <p class="text-lg font-semibold">
        “Tailwind CSS is the only framework that I've seen scale
        on large teams. It’s easy to customize, adapts to any design,
        and the build size is tiny.”
      </p>
    </blockquote>
    <figcaption class="font-medium">
      <div class="text-cyan-600">
        Sarah Dayan
      </div>
      <div class="text-gray-500">
        Staff Engineer, Algolia
      </div>
    </figcaption>
  </div>
</figure>
```

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

## CSS

<p align="center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/62/CSS3_logo.svg/240px-CSS3_logo.svg.png" height="256">
</p>

Just name your file with `.css` extension. Plain css, nothing to add

## SCSS

<p align="center">
    <img src="https://cdn.freelogovectors.net/wp-content/uploads/2019/02/sass-logo.png" height="256">
</p>

Just rename your file with `.scss` extension. **Create-react-app** template is configured to handle css preprocessors so your local setup will work just fine. On our side, your plugin will be build with special **webpack** config to include scss files. Use features provided by scss:

1. Reference symbol `&`

```scss
.block {
  &.red {
    color: red;
  }
}
```

1. `Variables`

```scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

3. Interpolation

```scss
$el: "post";
.#{$el} {
  background: blue;
  & .#{$el}__title {
    background: red;
  }
}
```

4. Functions and loops

```scss
$icons: smile, poop, godzilla;

@each $icon in $icons {
  .icon-#{$icon} {
    background-image: url("/icons/#{$icon}.png");
  }
}
```

5. `Mixins`

```scss
@mixin fight-with($monster) {
  @if $monster == mechagodzilla {
    .post__title {
      &:after {
        @content;
      }
    }
  } @else if $monster == spacegodzilla {
    @content;
  }
}
```

6. Placeholders `%`

```scss
%post-skeletor {
  font: {
    size: 12;
    weight: 700;
  }
  box-sizing: border-box;
  padding: 5px;
  margin: 10px;
  border: 1px solid whitesmoke;
}

.post-class {
  font: {
    size: 12;
    weight: 700;
  }
  box-sizing: border-box;
  padding: 5px;
  margin: 10px;
  border: 1px solid whitesmoke;
}

.post1--extends__placeholder {
  @extend %post-skeletor;
  background: yellow;
}

.post1--extends_class {
  @extend .post-class;
  background: yellow;
}
```

?> And many more features

## Module CSS

<p align="center">
    <img src="https://raw.githubusercontent.com/css-modules/logos/master/css-modules-logo.png" height="316">
</p>

This project supports CSS Modules alongside regular stylesheets using the [name].module.css file naming convention. CSS Modules allows the scoping of CSS by automatically creating a unique classname of the format [filename]\_[classname]\_\_[hash]

?> **Tip**: Should you want to preprocess a stylesheet with Sass then make sure to change the stylesheet file extension as follows: [name].module.scss or [name].module.sass.

Why use it?

1. No more naming conflicts
2. Explicit dependencies
3. No **global scope**

```scss
/* Button.module.css */
.error {
  color: red;
}
```

```scss
/* another-stylesheet.css */
.error {
  color: red;
}
```

```jsx
import React, { Component } from "react";
import styles from "./Button.module.css"; // Import css modules stylesheet as styles
import "./another-stylesheet.css"; // Import regular stylesheet

class Button extends Component {
  render() {
    // reference as a js object
    return <button className={styles.error}>Error Button</button>;
  }
}
```

```html
<button class="Button_error_ax7yz">Error Button</button>
```
