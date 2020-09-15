install node.js LS  
npm init -y (admin mode)  
npm install nodemon --save-dev  
npm install express  

modify package.json at scripts to "start": "nodemon"  


### node Package Manager

To exit npm start use:

        ctrl+V, ctrl+C

All of the CLI commands can be found at:

https://docs.npmjs.com/cli-documentation/cli

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

    npm install - g create-react-app -> now deprecated
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
    
### To avoid malicious packages installed through scripts:

`npm config set ignore-scripts true`
    
# 
### React

(previously create-react-app global should be preinstalled with:

`npm install - g create-react-app`)

installing dependencies with: 

```node
create-react-app <appname>
```
or: 

```node
npx create-react-app my-app
```

(in this case the app will be named my-app)

after installing dependencies:

cd in _app_folder_  

```node
npm start
```

NEED event emitter:

```node
npm i fbemitter
```


for simple-routing: 

```node
npm install --save react-router-dom
```

for redux:  
NEED redux, react-redux, primereact (custom components)

```node
npm install --save redux
npm install react-redux
npm install primereact --save
npm install primeicons --save
```

or better:

```node
npm i primereact primeflex primeicons react-transition-group classnames redux react-redux redux-promise-middleware redux-logger --save

npm i classnames --save
```


npm update -> update npm packages


Course "Integrarea serviciilor externe":
```node
npm i express request request-promise dotenv --save
```
