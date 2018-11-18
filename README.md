# The Legendary Manager Webapp

> Webapp of the best todo app evverrr

The webapp. React, GraphQL, Apollo Client.

## Getting started

This webapp is used together with [legendary-manager-api](https://github.com/cherrybeans/legendary-manager-api), so go ahead and set that one up if you want to run this properly.

### Setting up

I use `yarn`, but you may use `npm` instead with the equivalent commands.

Clone the project and install dependencies as such:

```sh
$ git clone git@github.com:cherrybeans/legendary-manager-webapp.git # or if not using ssh git clone https://github.com/cherrybeans/legendary-manager-webapp.git
$ cd legendary-manager-webapp
$ yarn # install the project dependencies
```

Then you can run the server with `yarn start` and go to [localhost:3030](http://localhost:3030) to view webapp.

### Useful scripts

In the project directory, you can run:

#### `yarn start`

> If you get an error mentioning that a module cannot be found, use the following command instead:
> `NODE_PATH=src/ && yarn start`
> This error happens because on some machines the configuration that gives us absolute imports is not being set correctly, and you need to manually set the config in your terminal.

Runs the app in the development mode. Open [http://localhost:3030](http://localhost:3030) to view it in the browser.

The page will reload if you make changes to the project. You will also see any lint errors in the console.

#### `yarn build`

Builds the app for production to the `build` folder. It correctly bundles React in production mode and optimizes the build for the best performance.

## A little noob guide on deploying on a Linux server

### Prerequisites

You'll need [node](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-18-04) and `yarn` (to make use of the lock file, though you may use npm).
You'll also need some tool to host it. We have used `Apache` to host this project. If you haven’t already installed it on your server, install it with `sudo apt install apache2` or use another tool.

### Frontend

First, make sure that `index.js` uses the production uri for linking the frontend to the server. It should be:

```js
const client = new ApolloClient({
  uri: "exampledomain.com:4000/graphql"
});
```

From your root folder, do the following:

```sh
$ yarn build
$ scp -r build <username>@exampledomain.com:~  # Copies the build folder to your home directory on the server
```

Then ssh into your server: `ssh <username>@exampledomain.com`.

```sh
$ sudo mv build /var/www/html/
$ sudo mv /var/www/html/build /var/www/html/prosjekt4
```

Now hopefully everything is up and running! The API should be up and running on [http://exampledomain.com:4000/graphql](http://exampledomain.com:4000/graphql).
