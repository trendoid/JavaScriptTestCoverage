[![MIT License](http://img.shields.io/badge/license-MIT-brightgreen.svg)](https://opensource.org/licenses/MIT) [![Build Status](https://travis-ci.org/trendoid/JavaScriptTestCoverage.svg?branch=master)](https://travis-ci.org/trendoid/JavaScriptTestCoverage)[![Coverage Status](https://coveralls.io/repos/github/trendoid/JavaScriptTestCoverage/badge.svg?branch=master)](https://coveralls.io/github/trendoid/JavaScriptTestCoverage?branch=master)
 
# JavaScript Test Coverage 
## a cozy blanket on a rainy day

### Testing Frameworks

There are choices when it comes to Javascript Testing Frameworks.  This particular app uses [Create React App](https://github.com/facebook/create-react-app) and uses [Jest](https://jestjs.io).

There are also choices when it comes to Coverage Frameworks.  Jest comes with [Instanbul](https://istanbul.js.org) built in.    

### Setup

Create a new React app

```
npx create-react-app my-app
cd my-app
npm start
```
After you've checked out the app and saw it running install a renderer.

```
yarn add --dev react-test-renderer
```
You can run coverage reports with a simple command or augment your `package.json` file to make it default.

```
npm test --coverage
```


### Extensions

There are probably extensions or visualizations for code coverage in your code edior. I use [VS Code](https://code.visualstudio.com) and like [Coverage Gutters](https://marketplace.visualstudio.com/items?itemName=ryanluker.vscode-coverage-gutters)

Most extensions work well with Istanbul but at the time I wrote this sample there were not a lot of working Jest extensions.
