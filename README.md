# threeflows
[![Build Status](https://travis-ci.org/mit-teaching-systems-lab/threeflows.svg?branch=master)](https://travis-ci.org/mit-teaching-systems-lab/threeflows)

A barebones [Express](http://expressjs.com/) server and [React](https://facebook.github.io/react/) webapp for doing design sketches of flows through a challenge and pieces of the challenge experience.  Code in both environments is written in [ES6](https://babeljs.io/docs/learn-es2015/).

## Server
#### Run locally
```
$ npm install
$ npm start
```

#### Database
It's expecting [Postgres](https://devcenter.heroku.com/articles/heroku-postgresql) in production, and doesn't use anything locally.

## UI
#### Tools
The project is built with [Browserify](http://browserify.org/) and uses Babel via [bablify](https://github.com/babel/babelify) to transpile ES6 and JSX.  It also uses [livereactload](https://github.com/milankinen/livereactload) for hot reloading of React components in local development.

For static analysis, we're experimenting with [eslint](http://eslint.org/) and [Flow](https://flowtype.org/).  The configuration for eslint uses [eslint-plugin-react](https://github.com/yannickcr/eslint-plugin-react) and [babel-eslint](https://github.com/babel/babel-eslint).  None of these tools trigger build failures right now, but can be run locally.

#### Watch and build with hot reloading
In another terminal, start process that will continually build the UI with hot reloading:
```
ui $ npm run watch
```
This builds artifacts and places them in the `ui/build` folder.

### Type check with Flow
This starts a [Flow](https://flowtype.org/) server in the background, and then runs a typecheck once.  There's no watch command right now.
```
ui $ npm run flow
``

### Run all tests
This is used in CI, and runs any and all tests in the project including typechecks.
```
ui $ npm run test
```

## Initial Heroku setup
Make sure you have [Node.js](http://nodejs.org/) and the [Heroku Toolbelt](https://toolbelt.heroku.com/) installed.  To run remote Postgres commands you'll also need to [install Postgres locally](https://devcenter.heroku.com/articles/heroku-postgresql).

Create the database:
```
$ heroku addons:create heroku-postgresql:hobby-dev
```

Seed the database:
```
$ heroku pg:psql
threeflows:DATABASE=> CREATE TABLE evidence (
  id serial primary key,
  app text,
  type text,
  version integer,
  timestamp timestamp,
  json jsonb
);
```

## Deploying to Heroku

```
$ heroku create
$ git push heroku master
$ heroku open
```
or

[![Deploy to Heroku](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

## Other services
[Travis](https://travis-ci.org/mit-teaching-systems-lab/threeflows) is setup for CI.  It will run on pull requests and on commits to master.

On merging to master, Travis will trigger a build.  If that build passes, Heroku will deploy the app on its own.

## Documentation

For more information about using Node.js on Heroku, see these Dev Center articles:

- [Getting Started with Node.js on Heroku](https://devcenter.heroku.com/articles/getting-started-with-nodejs)
- [Heroku Node.js Support](https://devcenter.heroku.com/articles/nodejs-support)
- [Node.js on Heroku](https://devcenter.heroku.com/categories/nodejs)
- [Best Practices for Node.js Development](https://devcenter.heroku.com/articles/node-best-practices)
- [Using WebSockets on Heroku with Node.js](https://devcenter.heroku.com/articles/node-websockets)
