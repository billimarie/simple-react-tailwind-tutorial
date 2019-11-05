# Tutorial: Make A Simple Website Using React & Tailwind CSS
A quick how-to guide for generating a simple, multi-page website.

## What You Need
- Terminal / Command Line
- IDE (I recommend [Atom](https://github.com/atom/atom))

### Versions
- Node: 8.11.3+
- npm: 6.12.1+

## Getting Started

**1. Initiate your React app using `create-react-app`:**
```
$ npx create-react-app react-tailwind-site
```

**2. Change directories into the app & install `react-router-dom` (for links), `tailwindcss` (for Tailwind CSS), `autoprefixer`, & `postcss-cli` (both are optional, but highly recommended for processing & watching your CSS.**
```
$ cd react-tailwind-site
$ npm install react-router-dom tailwindcss autoprefixer postcss-cli
```

**3. Test it out:**
```
$ npm run start
```
A new window should open up (`localhost:3000`) & display the standard new React App screen.

## Troubleshooting

- If you receive an error about serviceWorker.js, feel free to delete it.
