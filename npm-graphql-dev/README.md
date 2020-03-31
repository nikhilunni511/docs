# How to Setup a Apollo-server using  [graphql-dev](https://www.npmjs.com/package/graphql-dev "graphql-dev")

------------


### Features

- The [graphql-dev](https://www.npmjs.com/package/graphql-dev "graphql-dev") module make the developers effort less by auto generating an apollo-server by running a command.
- Using this module the developers can follow a modular approach through their project.

### Prequisites
- You should have Node and npm installed
- You should be familiar with Node, GraphQL and the npm ecosystem
- You have a code editor installed (preferably VS Code, it's the champ for TypeScript)

### Initial Setup
Let's create a folder for us to work in.


    mkdir apollo-server
    cd apollo-server
    
Next, we'll setup the project package.json and add the dependencies

### Setup Node.js package.json
Using the -y flag when creating a package.json will simply approve all the defaults.

`npm init -y`

### Add TypeScript as a dev dependency
`npm install typescript --save-dev`

After we install typescript, we get access to the command line TypeScript compiler through the tsc command.

### Create a tsconfig.json
The tsconfig.json is where we define the TypeScript compiler options. We can create a tsconfig with several options set.

Our **tsconfig.json** should look like this:


    {
        "compilerOptions": {
          "experimentalDecorators": true,
          "module": "commonjs",
          "esModuleInterop": true,
          "target": "es6",
          "moduleResolution": "node",
          "sourceMap": true,
          "outDir": "dist"
        },
        "lib": [
          "es2015"
        ],
        "experimentalDecorators": true
      }

We're set to run our first TypeScript file.

### Create the src folder
We are writing the code inside **src** folder excpet configurations.

`mkdir src`

After creating the src folder run the following command to generate a simple apollo server.

### Generate apollo server using graphql-dev
Run the following command :
`graphql-dev server`

After running the command you can see the following files in your src folder.
```
src
|		index.ts
|		modules.ts
|-------asoiaf
|		|		dataSource.ts
|		|		resolvers.ts
|		|		typeDefs.ts
|		|		index.ts
```

### Useful configurations & scripts
Cold reloading is nice for local development. In order to do this, we'll need to rely on a couple more packages: ts-node for running TypeScript code directly without having to wait for it be compiled, and nodemon, to watch for changes to our code and automatically restart when a file is changed.
`npm install --save-dev ts-node nodemon`

And then to run the project, all we have to do is run nodemon. Let's add a script in package.json for that.


    "scripts": {
       "start:dev": "nodemon src/index.ts",
    },

By running `npm run start:dev`, nodemon will start our app using ts-node ./src/index.ts, watching for changes to files from within /src.

Now the server is listening at http://localhost:3000.
###Images

Image:

![Sample output](docs/images/graphql_dev.png)

> Example 

### Creating production builds
In order to clean and compile the project for production, we can add a build script "build": " tsc" to your package.json


     "scripts": {
           "start:dev": "nodemon src/index.ts",
           "build": " tsc"
        },

Now, when we run `npm run build`, TypeScript compiler emits new code to dist.

### Production startup script
In order to start the app in production, all we need to do is run the build command first, and then execute the compiled JavaScript at build/index.js.

The startup script looks like this.
"start": "npm run build && node build/index.js"


    "scripts": {
               "start:dev": "nodemon src/index.ts",
               "build": " tsc",
               "start": "npm run build && node dist/index.js"
            },
