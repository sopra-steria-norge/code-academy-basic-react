# code-academy-basic-react

Målet med workshoppen her er at du skal få praktisk kjennskap til "legoklossene" vi har sett på underveis i kvelden.
For dere som har tidligere bygget enkle react-applikasjoner med f.eks "create-react-app" er det lett å ikke helt sette pris på hva som faktisk foregår i det du har kjørt "npm start" eller "npm run build".

I denne workshoppen skal går vi gjennom dette, steg for steg. Vi starter enkelt, og ønsker å sette opp en basic react app med typescript, som benytter seg av [webpack](https://webpack.js.org/) og [babel](https://babeljs.io/) for transpilering og bygg.

Merk at hovedpoenget her ikke er å bli først ferdig, men å roe ned og prøve å forstå hvorfor hvert steg i worlshopen gjøres, og hva de ulike delene gjør. Bruk lenkene godt og fordyp deg om det er noe du ikke forstår.

## Prerequisites

- [node med npm](https://nodejs.org/en)
- [git](https://git-scm.com/)

## Workshop

### 1. Sett opp en package.json med 

```bash
npm init -y
```
- [npm init](https://docs.npmjs.com/cli/v7/commands/npm-init)

### 2. Installer React og React DOM med kommandoen 

```bash
npm install --save react react-dom
```

- [react](https://www.npmjs.com/package/react) (npm)
- [react-dom](https://www.npmjs.com/package/react-dom) (npm)

### 3. Installer Typescript med 

```bash
npm install --save-dev typescript
```

- [typescript](https://www.npmjs.com/package/typescript) (npm)

Nå som vi har fått på plass typescript er det en god i de å dra med seg typedeklerasjoner for pakkene vi benytter for react koden vår, kjør 

```bash
npm i --save-dev @types/react @types/react-dom
``` 

- [@types/react](https://www.npmjs.com/package/@types/react) (npm)
- [@types/react-dom](https://www.npmjs.com/package/@types/react-dom) (npm)

Legg merke til `--save-dev`. Om dette er ukjent for deg ville jeg tatt meg tiden til å se raskt på hvordan NPM [strukturerer avhengigheter.](https://docs.npmjs.com/specifying-dependencies-and-devdependencies-in-a-package-json-file)

### 4. Sett opp en basic `tsconfig.json` og legg den på rotnivå av repo. For nå holder det med
  - [compilerOptions](https://www.typescriptlang.org/tsconfig/#compilerOptions)
    - [target](https://www.typescriptlang.org/tsconfig/#target)
    - [allowJs](https://www.typescriptlang.org/tsconfig/#allowJs)
    - [jsx](https://www.typescriptlang.org/tsconfig/#jsx)
    - [module](https://www.typescriptlang.org/tsconfig/#module)
    - [moduleResolution](https://www.typescriptlang.org/tsconfig/#moduleResolution)
    - [outDir](https://www.typescriptlang.org/tsconfig/#outDir)
    - [strict](https://www.typescriptlang.org/tsconfig/#strict)
    - [esModuleInterop](https://www.typescriptlang.org/tsconfig/#esModuleInterop)
  - [include](https://www.typescriptlang.org/tsconfig/#include)

```json
{
  "compilerOptions": {
    "target": "es6",
    "allowJs": true,
    "jsx": "react",
    "module": "nodenext",
    "moduleResolution": "nodenext",
    "outDir": "./dist",
    "strict": true,
    "esModuleInterop": true
  },
  "include": ["src/**/*"]
}
```

### 5. Installer `webpack` med 

```bash
npm install --save-dev webpack webpack-cli webpack-dev-server
```

- Webpack
  - [webpack](https://www.npmjs.com/package/webpack) (npm)
  - [webpack documentation](https://webpack.js.org/concepts)
- Webpack CLI
  - [webpack-cli](https://www.npmjs.com/package/webpack-cli) (npm)
  - [Webpack CLI documentation](https://webpack.js.org/api/cli)
- Webpack Dev Server
  - [webpack-dev-server](https://www.npmjs.com/package/webpack-dev-server) (npm)
  - [Webpack Dev Server documentation](https://webpack.js.org/configuration/dev-server)

### 6. Set opp `webpack.config.js` på rot

```js
const path = require("path");

module.exports = {
  mode: "development",
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

- [webpack](https://webpack.js.org/configuration)
  - [mode](https://webpack.js.org/configuration/mode)
  - [entry](https://webpack.js.org/configuration/entry-context/#entry)
  - [output](https://webpack.js.org/configuration/output)
  - [resolve](https://webpack.js.org/configuration/resolve)

### 7. Installer Babel og aktuelle presets

```bash
npm install --save-dev @babel/core babel-loader @babel/preset-env @babel/preset-react @babel/preset-typescript
```
- Babel/core
  - [@babel/core documentation](https://babel.dev/docs/babel-core)
  - [@babel/core](https://www.npmjs.com/package/@babel/core) (npm)
- Babel-loader
  - [babel-loader documentation](https://webpack.js.org/loaders/babel-loader)
  - [babel-loader](https://www.npmjs.com/package/babel-loader) (npm)
- Babel/preset-env
  - [@babel/core documentation](https://babeljs.io/docs/babel-preset-env)
  - [@babel/core](https://www.npmjs.com/package/@babel/preset-env) (npm)
- Babel/preset-react
  - [@babel/core documentation](https://babeljs.io/docs/babel-preset-react)
  - [@babel/core](https://www.npmjs.com/package/@babel/preset-react) (npm)
- Babel/preset-typescript
  - [@babel/core documentation](https://babeljs.io/docs/babel-preset-typescript)
  - [@babel/core](https://www.npmjs.com/package/@babel/preset-typescript) (npm)

### 8. Set opp en `.babelrc.json` fil

```
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react",
    "@babel/preset-typescript"
  ]
}
```

- [.babelrc.json](https://babeljs.io/docs/configuration#babelconfigjson)
  - [presets](https://babeljs.io/docs/presets)

La oss ta en fot i bakken og lese oss raskt opp på hva disse preset'ene faktisk inneholder og gjør. Les doc'en før du går videre!

- [babel-preset-env](https://babeljs.io/docs/babel-preset-env)
- [babel-preset-typescript](https://babeljs.io/docs/babel-preset-typescript)
- [babel-preset-react](https://babeljs.io/docs/babel-preset-react)

### 9. Oppdater `webpack.config.js`
 La oss integrere `webpack` og `babel`! Oppdater `webpack.config.js` til å inkludere følgende

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

- [webpack](https://webpack.js.org/configuration)
  - [module](https://webpack.js.org/configuration/module)
    - [rules](https://webpack.js.org/configuration/module/#modulerules)

### 10. Sett opp `./src/index.html`

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

### 11. Installer html-webpack-plugin
For å få webpack til å spille på lag med html-filen over trenger vi en ny plugin - html-webpack-plugin! Les deg opp på hva den gjør [her.](https://webpack.js.org/plugins/html-webpack-plugin/)

Installer den med:

```bash
npm install --save-dev html-webpack-plugin
```

- [HtmlWebpackPlugin](https://webpack.js.org/plugins/html-webpack-plugin) documentation
- [html-webpack-plugin](https://www.npmjs.com/package/html-webpack-plugin) (npm)

### 13. Oppdater `webpack.config.js` 
Oppdater `webpack.config.js` med den nye plugin'en, og pek den på filen vi opprettet over.

```js
// ...
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

### 14. Opprett en react-komponent
La oss opprette en enkel react-komponent - `./src/index.tsx`

```tsx
import React, { useState } from "react";
import ReactDOM from "react-dom/client";

const App: React.FC = () => {
  const [counter, setCounter] = useState(0);
  return (
    <div>
      <h2>Hei, verden! 😎</h2>
      <button onClick={() => setCounter(counter + 1)}>Klikk?</button>
      <p>Du har klikket på meg {counter} ganger🥵</p>
    </div>
  );
};

const rootElement = document.getElementById("root");
if (!rootElement) {
  throw new Error("root not found");
}
const root = ReactDOM.createRoot(rootElement);

root.render(<App />);
```

### 15. Oppdater `package.json``
Nå er alle småstegene underveis på plass, la oss oppdatere vår `package.json` til å dra nytte av oppsettet vårt! Legg til følgende:

```json
"scripts": {
  "start": "webpack serve --open",
  "build": "webpack --mode production"
}
```

- [webpack serve --open](https://webpack.js.org/configuration/dev-server/#devserveropen)
- [webpack --mode production](https://webpack.js.org/guides/production/#specify-the-mode)

### 17. Start applikasjonen
Start opp appen med `npm start`. Dette skal forhåpentligvis starte opp applikasjonen og åpne den opp i nettleseren din. Legg merke til at webpack vil lytte på endringer på filene dine og serve disse på nytt. Hot reload!
