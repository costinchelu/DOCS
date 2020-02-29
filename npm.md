install node.js LS  
npm init -y (admin mode)  
npm install nodemon --save-dev  
npm install express  

modify package.json at scripts to "start": "nodemon"  


### node Package Manager

To exit npm start use:

        ctrl+V, ctrl+C

All of the CLI commands can be found at: https://docs.npmjs.com/cli-documentation/cli

Used to initialize npm package.json at the start of a project

        npm init

For checking out npm or node installed versions:

        npm -v
        node -v
# 
### Packages to install:

_react (library used for interfaces)_

    npm install react
    npm install - g create-react-app
    create-react-app <appname>

    npm install - g create-react-app -> este acum deprecated
    se va folosi npx create-react-app <appname>

It will download files necessary for a React Project

_live-server_ (global installation) (it creates a fake server on localhost and automatically loads and refresh the project in the browser)

    npm install -g live-server

_lodash_ (installs only locally at project level)

    npm install lodash

When importing a new project, _package.json_ helps us to download all the needed dependencies by using command:

    npm install

All dependencies are written in the "dependencies" property and usually projects taken from Github will not include the actual dependencies which can be loaded by npm.

In the package.json "scripts" will help us run commands. For example:

    "scripts": {
    "build": "browserify working_with_files.js > bundle.js"
    }

The scripts can be run with:

    npm run build
    
# 
### React

(in prealabil create-react-app global trebuie sa fie preinstalat cu: npm install - g create-react-app)

instalam dependentele cu: 

```node
create-react-app <appname>
```
sau: 

```node
npx create-react-app my-app
```

(in acest caz, aplicatia va fi numită my-app)

dupa instalarea dependențelor:

cd in _directorul_aplicatiei_  

```node
npm start
```

instalam si un event emitter:

```node
npm i fbemitter
```


pentru simple-routing: 

```node
npm install --save react-router-dom
```

pentru redux:  
avem nevoie de redux, react-redux, primereact (pt componente custom)

```node
npm install --save redux
npm install react-redux
npm install primereact --save
npm install primeicons --save
```

sau mai bine:

```node
npm i primereact primeflex primeicons react-transition-group classnames redux react-redux redux-promise-middleware redux-logger --save

npm i classnames --save
```


npm update -> pentru update la pachetele npm


Cursul "Integrarea de servicii externe":
```node
npm i express request request-promise dotenv --save
```
