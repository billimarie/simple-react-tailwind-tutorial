# React Tutorials
> Updated: November 11th 2019

## Table of Contents
1. [Tutorial 1: A Simple Website with React, Tailwind CSS, & PostCSS](#tutorial-1)
1. [Tutorial 2: Adding CSS Transitions](#tutorial-2)

# Tutorial 1

Create a simple, multi-page website that watches your CSS changes & refreshes your app, accordingly.

To view the Medium.com article: [Creating A Simple Website with React, Tailwind CSS, & PostCSS](https://medium.com/clocktwine/creating-a-simple-website-using-react-tailwind-css-postcss-6bbc419ded0c)

## What You Need
- Terminal / Command Line
- IDE (I recommend [Atom](https://github.com/atom/atom))

### Versions
- Node: 8.11.3+
- npm: 6.12.1+

## Getting Started

### 1. Initialize your React app using `create-react-app`:
```
$ npx create-react-app react-tailwind-site
```

### 2. Change directories into the app & install `react-router-dom` (for links), `tailwindcss` (for Tailwind CSS), `autoprefixer`, & `postcss-cli` (to watch & reload CSS updates):
```
$ cd react-tailwind-site
$ npm install react-router-dom tailwindcss autoprefixer postcss-cli
```

### 3. Test it out:
```
$ npm run start
```
A new window should open up (`localhost:3000`) & display the standard new React App screen.

(Having trouble? See [Troubleshooting](#troubleshooting)).

## Setting Up Tailwind

### 1. Initialize Tailwind & PostCSS:
```
$ npx tailwind init tailwind.config.js
```

### 2. Create Tailwind.css:
```
$ cd src ; mkdir css ; cd css ; touch tailwind.css // Linux
$ cd src & mkdir css & cd css & touch tailwind.css // Windows
```

### 3. Add to `src/css/tailwind.css`:
```
/* Init Tailwind */
@tailwind base;

@tailwind components;

@tailwind utilities;

/* Custom CSS */
```

## Connecting Tailwind & React

### 1. Modify your `package.json` with these updated scripts:
```
"scripts": {
    "build:css": "postcss src/css/tailwind.css -o src/index.css",
    "watch:css": "postcss src/css/tailwind.css -o src/index.css -w",
    "start": "npm watch:css & react-scripts start",
    "build": "npm run build:css && react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
}
```

### 2. Modify `App.js`:
```
import './css/tailwind.css';     /* Replacing App.css */
```

### 3. Modify `index.js`:
```
import './index.css';    /* Replacing App.css */
```

### 4. Let's restart the app!
```
$ npm run start
```

You should see an updated `localhost:3000` page.

To test that it's watching your CSS changes, go back to `src/css/tailwind.css` & add a new style under "Custom CSS." Your app should refresh with the changes automatically:

![react-tailwind-watching-loop](https://user-images.githubusercontent.com/6895471/68322467-44e2a100-0078-11ea-811e-13f8456cdf5f.gif)

## Creating Components

### 1. Create a folder called "Components." It should be in your source files (`/src/components/`)
```
$ mkdir components
```

### 2. To start off, let's build a header.
```
$ cd src/components ; touch Header.js // Linux
$ cd src/components & touch Header.js // Windows
```

### 3. In Header.js:
```
import React from 'react';
import {
  BrowserRouter as Router,
  Switch,
  Route,
  Link } from 'react-router-dom';

const Header = () => (
  <header className="bg-gray-100 p-6">
    <div className="flex items-center justify-between flex-wrap">
      <div className="block">
        <Link to="/"><span className="font-semibold text-xl tracking-tight text-gray-800">Title Goes Here</span></Link>
      </div>
      <nav className="block">
        <Link to="/"><span className="inline-block text-gray-800 hover:text-gray-600 mr-4">Home</span></Link>
        <Link to="/"><span className="inline-block text-gray-800 hover:text-gray-600 mr-4">About</span></Link>
        <Link to="/"><span className="inline-block text-gray-800 hover:text-gray-600 mr-4">Contact</span></Link>
        <Link to="/"><span className="inline-block px-4 py-2 leading-none border rounded text-gray-600 border-gray-600 hover:text-gray-900 hover:border-gray-900">Login</span></Link>
      </nav>
    </div>
  </header>
);
export default Header;
```

### 4. Go to `App.js` and add the following imports
```
import {
  BrowserRouter as Router,
  Switch,
  Route,
  Link
} from 'react-router-dom';
import Header from './components/Header.js';
```

Scroll down and replace the content React automatically generated with the following:
```
const App = () => (
  <Router>
    <Header />
  </Router>
);
export default App;
```

### 5. Now that we've made the universal header, let's create the pages for Home, About, & Contact:
```
$ touch Home.js About.js Contact.js
```

Open `Home.js` add the following:

```
import React from 'react';

const Home = () => (
  <h2>Home</h2>
);

export default Home;
```

You can reuse this code for your `About.js` and `Contact.js` pages.

### 6. Again, back to `App.js` to import your new components:

```
import Home from './components/Home.js';
import About from './components/About.js';
import Contact from './components/Contact.js';
```

Scroll down to modify:

```
<Router>
  <Header />
  <Switch>
    <Route exact path="/">
      <Home />
    </Route>

    <Route exact path="/about">
      <About />
    </Route>

    <Route exact path="/contact">
      <Contact />
    </Route>
  </Switch>
</Router>
```

### 7. Modify `index.js` to activate the router:
```
import { BrowserRouter } from 'react-router-dom';

ReactDOM.render(<BrowserRouter><App /></BrowserRouter>, document.getElementById('root'));
```

### 8. You're all set! Restart the app to see your new changes.
```
$ npm run start
```

You should be able to see the new header, and click on each navigation item to take you to a new page:

![react-tailwind-links](https://user-images.githubusercontent.com/6895471/68329481-27b4cf00-0086-11ea-93ee-580fcef18c6e.gif)

## Complete!

If you get stuck or have any questions, feel free to send me a message. I'd love to see what you create with this; submit a pull request with your screenshot or link to be added to this GitHub repo.

## Troubleshooting

- If you receive an error about ServiceWorker.js, go to `index.js` and comment it out. (You can also delete the file itself under `src/serviceWorker.js`.)
- Additionally, if you're running Windows, make sure system32 has been added to your PATH (see: [this GitHub issue](https://medium.com/r/?url=https%3A%2F%2Fgithub.com%2Ffacebook%2Fcreate-react-app%2Fissues%2F7061)).

([Back to Top](#react-tutorials))

# Tutorial 2

Adding CSS Transitions.

## Getting Started

### 1. Add `React Transition Group`:
```
$ npm install react-transition-group --save-dev
```

### 2. Import in your chosen view (I picked `Home.js`):
```
import { CSSTransition } from 'react-transition-group';
```

### 3. Declare new consts: 
```
const [showVertical, setShowVertical] = useState(true),
      [showHorizontal, setShowHorizontal] = useState(false);
```
