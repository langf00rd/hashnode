## How To Create A React Component Library

If you're reading this, I assume you're familiar with UI component libraries such as Material UI, Ant Design, Semantic UI, Chakra UI, and others. These libraries provide components like Buttons, Popups, Labels. Spinners, Loaders, etc.

Luckily, setting up a similar React UI component-based library is pretty simple, allowing you to create reusable components that can be imported and used in any React project. This article will walk you through the process of creating a React component library step by step.

## Getting started

Creating our folder structure may be difficult, so we will take the easy way out. We'll be using the CLI tool [create-react-library](https://www.npmjs.com/package/create-react-library).

This tool configures our project with Rollup, Babel, and Jest for bundling, transpiling, and testing. It also allows our project to support TypeScript, complex peer dependencies, and CSS modules.

## Installing create-react-library

This package requires Node version 10 or higher. The most recent Node version can be downloaded from the official NodeJs [downloads page](https://nodejs.org/download/release/latest/).

Install `create-react-library` by running the following command from your terminal:

```
npm install -g create-react-library 
```

## Creating the folder structure

Now that we've installed `create-react-library`, we can run the command below to create our project. For this tutorial, we'll name our project as `test-library`. You can change the name to whatever you want. 

```
create-react-library test-library
```

Or with npx:

```
npx create-react-library test-library
```

You will be required to enter a:
- Package Name
- Package Description
- Author's GitHub Handle
- GitHub Repo Path
- License
- Package Manager
- Template

When you open the newly created project in your text editor, you should see the same folder and file structure. If something doesn't seem right, repeat the preceding command.

![project folder structure screenshot](https://res.cloudinary.com/follio/image/upload/v1660492811/escfkqzapfvjvnzerl59.png)

The package creates a local repository and links the packages together, allowing us to view and test our components locally. That's pretty cool.

## Development

Our local development is divided into two separate parts:

- Using rollup to watch and compile our code from `src/` into the `dist/` folder
- Running and listening from changes in the `example/` react project

### Running the example react app

A basic react app that has already been linked to the library we're creating can be found in the example/ folder. Run the react app dev server by:

```
cd example # change directory into the example/ folder
npm start # runs a dev server for the react app
```

You might get an error like this:

```
{
  ...
  library: 'digital envelope routines',
  reason: 'unsupported',
  code: 'ERR_OSSL_EVP_UNSUPPORTED'
}
```

If you do, open the `package.json` file in the `example/` folder and change the default script object to:

```
"scripts": {
    "start": "node ../node_modules/react-scripts/bin/react-scripts.js --openssl-legacy-provider start",
    "build": "node ../node_modules/react-scripts/bin/react-scripts.js --openssl-legacy-provider build",
    "test": "node ../node_modules/react-scripts/bin/react-scripts.js --openssl-legacy-provider test",
    "eject": "node ../node_modules/react-scripts/bin/react-scripts.js --openssl-legacy-provider eject"
  },
```

When you go to `localhost:3000/` in your preferred browser, you should see this.

![react app](https://res.cloudinary.com/follio/image/upload/v1660494275/uqity9ghrcocaxgqlrny.png)

### Running the main component code

In the base directory, run this piece of code to watch for changes and compile the code from our `src/` folder in real-time

```
npm start # runs rollup with the watch flag
```


## The Component's Code

A sample component `ExampleComponent` has been created for us in the base directory's `src/` folder. This component takes a `text` property and renders a simple UI, as seen in the browser.

```
import React from 'react'
import styles from './styles.module.css'

export const ExampleComponent = ({ text }) => {
  return <div className={styles.test}>Example Component: {text}</div>
}

```

The styles for the component can be found in the `styles.module.css` file. From here, you can style your component however you want.

```
/* add css module styles here (optional) */

.test {
  margin: 2em;
  padding: 0.5em;
  border: 2px solid #000;
  font-size: 2em;
  text-align: center;
}

```

Our component(s)' compiled code can be found in the dist folder. This is the folder that will be deployed to npm

![Dist folder screenshot](https://res.cloudinary.com/follio/image/upload/v1660495468/scwtx4wozwot0bmyhsyc.png)

## The Frontend Code


In the `example/src/App.js` file, our library is imported together with the CSS file containing all of our stylings.

```
import React from 'react'

import { ExampleComponent } from 'test-library'
import 'test-library/dist/index.css'

const App = () => {
  return <ExampleComponent text="Create React Library Example 😄" />
}

export default App

```

## Publishing our project to npm

We run the following command to generate a `commonjs` and `es` version of our code, push it to the `dist/` folder, and publish it to npm:

```
npm publish
```

Thats it!

## Deploying to GitHub Pages

```
npm run deploy
```

This generates a build version of our `example/` react app in which we imported and displayed our components.

## Final words

We've created our very own react component library that can be imported and used in any react project.

Milky UI is an open source react UI component project I'm working on. I created the project using the same method. The code is available on [GitHub](https://github.com/langford-dev/milky-ui/). It is also available on [npm](https://www.npmjs.com/package/milky-ui)

I hope you found this post useful. See you in the next article