[![MIT License](http://img.shields.io/badge/license-MIT-brightgreen.svg)](https://opensource.org/licenses/MIT)   [![Build Status](https://travis-ci.org/trendoid/JavaScriptTestCoverage.svg?branch=master)](https://travis-ci.org/trendoid/JavaScriptTestCoverage)   [![Coverage Status](https://coveralls.io/repos/github/trendoid/JavaScriptTestCoverage/badge.svg?branch=master)](https://coveralls.io/github/trendoid/JavaScriptTestCoverage?branch=master)
 
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

After you've checked out the app and saw it running, install a renderer.
```
yarn add --dev react-test-renderer
```

You can now run unit tests right away locally.  Jest is built into create-react-app.
```
npm test
```

You can run coverage reports with a simple command or augment your `package.json` file to make it default.
```
npm test --coverage
```

Lets go ahead and add a `jest` section to the `package.json` file with some exclusions and some reporters.
```json
"jest": {
    "collectCoverageFrom": [
        "**/*.{js,jsx}",
        "!**/index.js",
        "!**/serviceWorker.js",
        "!**/build/**",
        "!**/node_modules/**",
        "!**/vendor/**"
    ],
    "coverageReporters": [
        "json",
        "lcov",
        "html"
    ]
}
```

That's cool and all but no one really gets to see that unless they download the code, build and test it.

Lets get a build server.  You don't want to just trust that it builds on your machine do you?

For this project we are going to use [Travis CI](https://www.travis-ci.com/).  Before we go there, lets add a [Yaml](https://yaml.org/) file called `.travis.yml`

In it we'll add:
```yaml
language: node_js
node_js:
  - 10
cache:
  directories:
    - node_modules
script:
  - npm run build
  - npm test
```
Then log in to Travis CI, connect it to your Github account or whereever, find your repository and finish setting it up.

Travis CI makes things so easy, I'm not going to cover that.

After Travis, we have to set up [Coveralls](https://coveralls.io).  Coveralls will automate our code coverage reporting and create a badge that we can put in our README or any place we want.

Install coveralls so we can report locally later if we want.
```
yarn add --dev coveralls
```

Let's exclude `/coverage` and `.coverall.yml` from our Git repo.  If someone wants to see coverage they'll just use Coveralls.

Add these lines to your `.gitignore` file.
```	
coverage
.coveralls.yml
```

If you need to upload local coverage reports to Coveralls then you'll follow the instructions to set that up add add a token to `.coveralls.yml`.  Don't ever upload tokens to public repositories.

Lets add some more scripts to our `package.json` file.

```
    "coverage": "react-scripts test --coverage",
    "coveralls": "cat ./coverage/lcov.info | node node_modules/.bin/coveralls",
```

We have to make sure that Travis executes the coverage tests by editing the `.travis.yml` file.  Here is our new Yaml file.

```yaml
language: node_js
node_js:
  - 10
cache:
  directories:
    - node_modules
script:
  - npm run build
  - npm test
  - npm run coverage
after_success: 'npm run coveralls'
```

Once everything is pushed to the repository, the repositories are activated in Travis and Coveralls. You'll see cool little badge icons that you can use for your README's or any place you want to use them.

### Extensions

There are probably extensions or visualizations for code coverage in your code edior. I use [VS Code](https://code.visualstudio.com) and like [Coverage Gutters](https://marketplace.visualstudio.com/items?itemName=ryanluker.vscode-coverage-gutters)

Most extensions work well with Istanbul but at the time I wrote this sample there were not a lot of working Jest extensions.
