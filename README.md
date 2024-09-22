# code-academy-basic-react

Målet med workshoppen her er at du skal få praktisk kjennskap til "legoklossene" vi har sett på underveis i kvelden.
For dere som har tidligere bygget enkle react-applikasjoner med f.eks "create-react-app" er det lett å ikke helt sette pris på hva som faktisk foregår i det du har kjørt "npm start" eller "npm run build".

I denne workshoppen skal går vi gjennom dette, steg for steg. Vi starter enkelt, og ønsker å sette opp en basic react app med typescript, som benytter seg av [webpack](https://webpack.js.org/) og [babel](https://babeljs.io/) for transpilering og bygg.

Merk at hovedpoenget her ikke er å bli først ferdig, men å roe ned og prøve å forstå hvorfor hvert steg i worlshopen gjøres, og hva de ulike delene gjør. Bruk lenkene godt og fordyp deg om det er noe du ikke forstår.

## Prerequisites

- [node med npm](https://nodejs.org/en)

## Workshop

1. Sett opp en package.json med `npm init -y`
2. Installer React, React DOM med kommandoen `npm install --save react react-dom`
3. Installer Typescript med `npm install --save react react-dom`
4. Sett opp en basic `tsconfig.json`, for nå holder det med

```json
{
  "compilerOptions": {
    "target": "es5",
    "allowJs": true,
    "jsx": "react",
    "moduleResolution": "node",
    "outDir": "./dist",
    "strict": true,
    "esModuleInterop": true
  },
  "include": ["src/**/*"]
}
```

5. Installer `webpack` med `npm install --save-dev webpack webpack-cli webpack-dev-server`
6. Set opp `webpack.config.js` på rot

```js
const path = require("path");

module.exports = {
  entry: "./src/index.tsx",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname, "dist"),
  },
  resolve: {
    extensions: [".tsx", ".ts", ".js"],
  },
};
```

7. Installer Babel og aktuelle presets `npm install --save-dev @babel/core babel-loader @babel/preset-env @babel/preset-react @babel/preset-typescript`
8. Set opp `.babelrc` fil

```
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react",
    "@babel/preset-typescript"
  ]
}
```

La oss ta en fot i bakken og lese oss raskt opp på hva disse preset'ene faktisk inneholder og gjør. Les doc'en før du går videre!

- [babel-preset-env](https://babeljs.io/docs/babel-preset-env)
- [babel-preset-typescript](https://babeljs.io/docs/babel-preset-typescript)
- [babel-preset-react](https://babeljs.io/docs/babel-preset-react)

9. La oss integrere `webpack` og `babel`! Oppdater `webpack.config.js` til å inkludere følgende

```js
// ...
module.exports = {
  // ...
  module: {
    rules: [
      {
        test: /\.(ts|tsx)$/,
        exclude: /node_modules/,
        use: "babel-loader",
      },
    ],
  },
};
```

10. Sett opp `./src/index.html`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Code Academy - React</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

11. For å få webpack til å spille på lag med html-filen over trenger vi en ny plugin - html-webpack-plugin! Les deg opp på hva den gjør [her.](https://webpack.js.org/plugins/html-webpack-plugin/)
12. Installer den `npm install --save-dev html-webpack-plugin`
13. Oppdater `webpack.config.js` med den nye plugin'en, og pek den på filen vi opprettet over.

```js
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  // ...
  plugins: [
    new HtmlWebpackPlugin({
      template: "./src/index.html",
    }),
  ],
};
```

14. La oss opprette en enkel react-komponent - `./src/index.tsx`

```tsx
import React from "react";
import ReactDOM from "react-dom/client";

const App: React.FC = () => {
  return <div>Hei, verden!</div>;
};

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<App />);
```

15. Nå er alle småstegene underveis på plass, la oss oppdatere vår `package.json` til å dra nytte av oppsettet vårt! Legg til følgende:

```json
"scripts": {
  "start": "webpack serve --open",
  "build": "webpack --mode production"
}
```

16. Start opp appen med `npm start` og hopp inn i http://localhost:8080
17. Viola!
