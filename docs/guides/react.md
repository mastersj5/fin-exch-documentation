# React Development

The React frontend is located at `/client/frontend/`, and any file paths referenced in this doc will be rooted at that path. I.E, `/src/index.tsx` refers to `/client/frontend/src/index.tsx`.

<!-- prettier-ignore-start -->
| Table of Contents                                                       |
| ----------------------------------------------------------------------- |
| [1. Starting up the project](#starting-up-the-project)                  |
| [2. Components](#components)                                            |
|   - [React Components](#react-components)                               |
|   - [Rules](#rules)                                                     |
|   - [*.module.scss](#modulescss)                                        |
|   - [*.props.ts](#propsts)                                              |
|   - [*.tsx](#tsx)                                                       |
|                                                                         |
| [3. Bootstrap and other Styling Considerations](#bootstrap-and-other-styling-considerations)                             |
| [4. Hooks](#hooks)                                                     |
| [5. Coding Standards](#coding-standards)                                |
<!-- prettier-ignore-end -->

## Starting up the project

In a terminal

```
$ cd client/frontend
$ npm i
$ npm run start
```

## Components

Components are an essential part to many mainstream javascript frameworks, including React, Angular, Vue, and Vite. The idea is to identify parts of a website that can be reused. A good example of this is a card that displays information about an object. You don't want to rewrite what boils down to the same code over and over again. You can write it once, and use it across the rest of the app. To identify a component, identify "objects." Components should also adhere to the "single-responsibility" principle. In other words, it should do one thing and do it really well.

### React Components

In this project, react components are all located in `/src/components/`, and each component get its own folder. `/src/components/button` holds all of the files relating to the `Button` component.

Generally speaking, there will be three files per component - though several more can and will exist depending on the complexity. The three most common files will be `component.tsx`, `component.module.scss`, and `component.props.ts`.

#### Rules

1. All components must begin with a capital letter
1. A component must return/render exactly ONE root element. If you have to render two sibling elements, you may wrap them with an empty tag `<>...</>`, or more explicitly, with `<Fragment>...</Fragment>`.

#### \*.module.scss

SCSS Modules are special because they encapsulate styles to that component. If two components have elements with a CSS class called `my-button` contained within them, they will be styled according to their respective `*.module.scss` files. If you would like a style to be added globally, add it to the `/styles/styles.scss` file.

Note: This file **must** be imported in the `.tsx` file. Instructions for this will be discussed in the respective section.

#### \*.props.ts

Props files define the options a component can take in. React has two primary "special" props.

```ts
children: ReactNode,
className: string
```

`children` is a special prop that allows you to render elements as children of the component. Our Button has an example of this. It takes a `children` prop, which will accept any text or html elements and display it within the button. Take a look at the `button.tsx` file to better understand this.

`className` allows you to specify css classes on your elements. `className` must be applied to an element that is rendered within your component. This will typically be the root element.

```ts
export const MyComponent = (props: MyProps) => {
  //...
  return <div className={props.className}>...</div>;
};
```

Any number of other props can be defined to help manage state or customize your component.

#### \*.tsx

TSX files define the component itself. These files define what the component will look like, and manage state. The following is a typical example of a `tsx` file's structure. `/components/button/button.tsx` is a complete example.

```tsx
import styles from "./my-component.module.scss";
import { MyProps } from "./my-component.props.ts";
import { useState } from "React";

export const MyComponent = (props: MyProps) => {
  const [count, setCount] = useState(0);

  function doSomething() {
    // I do something really important.
  }

  return (
    <>
      <button
        className={`${props.className}`}
        onClick={() => setCount(count + 1)}>
        Click Me
      </button>
      <div>Count: {count}</div>
    </>
  );
};
```

Notice a few things:

1. SCSS styles are imported as shown on line one of the above snippet
1. State is defined at the top of the component
1. The component name (`MyComponent`) is capitalized
1. Curly brackets {} break back into Javascript, and will render the results to the DOM.
1. Javascript interactivity can be defined inline (`onClick={() => setCount(count + 1)}`)

The last point is especially important for user-interactivity. It is generally preferred to inline your code as shown, if the code is simple. For more complex tasks, define a function such as `doSomething()`, and call it like `onClick={() => doSomething()}`.

## Bootstrap and other Styling Considerations

- - Bootstrap is being used in this project, and a lot can be overridden without having to override each class. A full list of bootstrap's variables can be found [here](https://getbootstrap.com/docs/5.0/customize/css-variables/#root-variables).

Reactstrap has been added to this project as well, which provides prebuilt components using Bootstrap. `<Row />`, `<Col />`, etc are available. The primary benefit is less typing, and the addition of intellisense to help know what options are available to you.

- Variables should be overridden in `/src/styles/variables.scss`.

- To override `--bs-primary`, write `$primary: #FFFFFF;`. This will apply to any `*-primary` classes, i.e. `btn-primary`, `text-primary`, `bg-primary`, etc.

- Global styles should be added to `/src/styles/styles.scss`, but more specific styles should be relegated to the closest `*.module.scss` file.

- React requires the root CSS selector to be a class name. In other words, it is not possible to directly target an element or an id.

- This project is using `scss`, which is a superset of `css`. It is completely opt-in, which means normal `css` syntax will work without issue. However, `scss` provides additional features such as variables and the ability to nest selectors. [Click here](https://sass-lang.com/) for more information about SASS/SCSS.

  ```scss
  .my-class {
    #my-id {
    }
  }
  ```

  is equivalent to

  ```css
  .my-class > #my-id {
  }
  ```

## Hooks

Hooks are a major concept in React, and provide the facilities for maintaining state. There aren't many built in, and the most commonly used ones are relatively easy to understand. The most important ones are `useState`, and `useEffect`. The former is used to manage state/variables that are rendered to the screen, and the latter is typically used to make calls to APIs, or to respond to changes in state. Check out the [docs](https://react.dev/reference/react/hooks) for more info.

A few key points however:

1. All hooks in React start with `use`
1. Hooks must be the first things called in a component
1. Hooks cannot be nested within functions
1. Custom hooks can be made to make recurring functionality easier to implement

## Coding Standards

There are a few standards we can use to make development easier for everyone. These will be enforced during Pull Requests, and align with industry best-practices.

1. Comment functions, props, or public members. Check `/src/components/button` for a fully-commented example.
1. Have [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) installed in VSCode.
1. Do not have unnamed colors in CSS files. Hex-codes should only be present in the `/src/styles/variables.scss` file.
1. If an HTML tag does not have any children, self-close it. (`<Element />` is correct, `<Element></Element>` is not.)
