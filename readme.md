# Front End Web Development 
This document is intended to cover the aspects required to write front-end production code. Let me know what you think, if I've missed anything or represented anything incorrectly - happy to hear any feedback!
​
Contents: 
- React 
- Redux
- Redux Middleware (saga / thunk)
- TDD
- Testing (jest / enzyme / react-testing-library)
- Typescript 
- Integration Testing 
- XUI
- Tooling
- create-xero-app
- Example of a basic app 
- Getting a project set up

#### Ideally it would be best to start writing your react application with typescript, redux and TDD from the get-go. I.e. refactoring local component state into global redux state is a pain.
​
Useful guides to know what is the current best languages and frameworks:
- https://www.thoughtworks.com/radar/languages-and-frameworks  
- https://techradar.xero-support.com
​
---
## React 
React is the main frontend framework used at Xero. Using the JavaScript language, it can produce instantaneous changes in state in the browser for the user - without having to reload the page. It uses a concept of "components" which allow us to seperate out complex logic. 
​
React cheat sheet, including:
- create-react-app (easiest way to start a react app)
- react router
- hooks 
- fragments
​
React cheat sheet: 
​
- https://gist.github.com/Mark-Cooper-Janssen-Vooles/f599220cd507a6f8416e870612ae3f2a
​
An example of using a react class component vs a functional component:
- https://gist.github.com/Mark-Cooper-Janssen-Vooles/81d4bec9d7bb8dd32d0933c5d26f4ecb
​
React documentation can be found here:
- https://reactjs.org/docs/getting-started.html
​
---
## Redux 
When a react application gets complex, changes in state are best managed by Redux (a global state, avoids having to noodle state through components).
​
It does this essentially by creating a initial state object, a reducer and actions. The current state is passed into the reducer along with an action, which causes the current state to change. Components that need access to this state must be connected, with props and actions added appropriately. For async calls to a back end, middleware is used.
​
Redux cheatsheet:
- https://gist.github.com/Mark-Cooper-Janssen-Vooles/822a49012315a24f9f3e1cd2e9b8fc69
​
Redux documentation can be found here:
- https://redux.js.org/introduction/getting-started
​
---
## Redux Middleware 
Redux middleware is used for async calls to a backend, and allows actions to return a function after a promise has been resolved.
​
Two popular middleware include 'redux-thunk', which is good for smaller applications, mentioned here: 
- https://gist.github.com/Mark-Cooper-Janssen-Vooles/822a49012315a24f9f3e1cd2e9b8fc69
​
Redux-thunk:
- https://github.com/reduxjs/redux-thunk
​
And 'redux-saga' better for larger applications, with a redux saga cheatsheet: 
- https://gist.github.com/Mark-Cooper-Janssen-Vooles/6f62f815732389eb53f69adda11ddd2f
​
Redux-saga:
- https://redux-saga.js.org/
​
---
## TDD - Test Driven Development 
TDD is only for unit tests.
Ideally all applications are created by TDD, or there is testing on every component and piece of logic that is written. 
​
The essence of TDD is:
- Write unit tests first, then write code that passes the test 
- The tests drive the development
- Produces clean optimal code, easy to read
- An automatic verification that the software works 
- The advantage of TDD is not increased productivity, but the long-standing feedback of the code 
​
When writing unit tests, plan things out as to what type of tests you can foresee coming up. Know what to test. 
​
3 Rules of TDD: 
1. Only write enough of a unit test to make the test fail
2. Only write enough code to make the failing test pass 
3. Repeat 
​
Use the arrange, act, assert style. 
​
---
## Testing - Jest / Enzyme / React-testing-library
When starting a new react project with 'create-react-app' you can start writing tests straight away. React-testing-library is currently the industry accepted gold standard for testing react. 
​
When testing a react app, you can shallow render or mount render a component. Shallow rendering is a "true" unit test as it isolates that component without including any children components, where as mount includes children components. 
When using the xero XUI library, often mount has to be used and there are issues with shallow rendering. 
​
What to test: 
- If an element is present or not
- If a class is being correctly applied to the element 
- If the correct text exists in the component
- If the component being rendered matches the snapshot
- If the props are updating correctly 
- If the elements are present or not given the props (i.e. a hidden={true} prop should not be present)
- If any events (i.e. onClick, onChange etc) update correctly. This could be a state change, a text change, a class change etc 
- All redux actions should be tested
- Defaults have the correct state upon mounting
- APIs are mocked and called with correct arguments 
​
Jest + Enzyme examples:
- https://gist.github.com/Mark-Cooper-Janssen-Vooles/45ef312d512c2287170d5dddd4cfc666
​
Jest: 
- https://jestjs.io/docs/en/getting-started
​
React testing library:
- https://testing-library.com/docs/react-testing-library/intro
- Good blog post: https://www.robinwieruch.de/react-testing-library
​
---
## Typescript
Typescript simply adds types to JavaScript, making the code less likely to break and pointing out potential bugs before they occur. Its use is increasingly more popular in production code. 
Similar to TDD, it may slow productivity but makes the code more robust. 
​
Typescript cheatsheet: 
- https://gist.github.com/Mark-Cooper-Janssen-Vooles/c15fc13119c484731daa650ef5e48d58
​
Typescript:
- https://www.typescriptlang.org/docs/home
​
---
## Integration Testing 
Frameworks used for integration testing include Nightwatch and Cypress. Currently cypress is rated the gold standard, but there are many integration tests using Nightwatch. 
​
Integration tests interact with the browser, mimicking the actions of a user. 
​
Integration testing cheatsheet: 
Integration tests in nightwatch will have a before and after section, with functions to execute before the tests are run and after. 
​
The developer guide has basic information on how to run an automation test: https://nightwatchjs.org/guide
Note that it is best to understand this, but also to follow the conventions found in the existing repo.
​
Things to watch out for: 
- Generally speaking you need to make sure the tests you write return the state to how it was before you touched it. 
- Time outs => you need to make timeouts as robust as possible. If you are attempting to generate a report or something of that nature, it might be best to use a polling function and has maybe 10 tries. Also of note, do not use things like .pause(5000) - what if it takes longer than 5 seconds? Instead opt for things like .waitForElementPresent before usinga .click
- Its best to make a model and export any complex logic to this, including element selectors etc. 
​
Nightwatch:
- https://nightwatchjs.org/guide
​
Cypress:
- https://www.cypress.io/
​
---
## XUI
XUI is the CSS framework that xero uses. It has two main sections, normal CSS XUI and react component XUI. When creating a new xero page or component, you need to check the XUI version found in the package.json and make sure the documentation you are viewing matches with that one. 
​
Generally the process will be an import at the top of the react file, followed by the use of the imported component in the JSX being rendered. Each react xui component will be different and accept different props to be passed in - you need to follow the docs closely. 
​
To style or arrange the page, you can just the normal CSS XUI to apply styles to the className. This would include things like XUI flex. Sometimes the documentation is not straight forward, for example when you want to make something into a flexbox with children space-between, you need to use both xui-u-flex AND xui-u-flex-justify-space-between, i.e: ``className="xui-u-flex xui-u-flex-justify-space-between"``. It may require some fiddling.
- https://xui.xero.com/16.5.0/section-fundamentals-utilities.html#fundamentals-utilities-1
​
The documentation for normal CSS XUI can be found at https://xui.xero.com, and for react XUI https://xui.xero.com/16.5.0/react/
​
---
## create-xero-app
create-xero-app is essentially Xero's own version of create-react-app. The repo lives here: https://github.dev.xero.com/Xero/create-xero-app
Right now the version in the repo instructions is broken, but the latest version works: 
To get the latest version in the master branch, run ``npx git+https://github.dev.xero.com/Xero/create-xero-app <project-name>``, otherwise follow instructions in the repos readme.
​
---
## Tooling
//todo still! 
npm, eslint babel, prettier, webpack
​
---
## Example of a basic app
This app was created using the above principles this:
- https://github.dev.xero.com/mark-janssen-vooles/quote-app-frontend
​
---
## Getting a project set up 
Get the basic app set up:
- ``npx git+https://github.dev.xero.com/Xero/create-xero-app <project-name>``
​
Add typescript: 
- ``npm install --save typescript @types/node @types/react @types/react-dom @types/jest @types/react-router-dom @types/react-redux``
- If you get red underlines as you're coding, you may need to install other typess
​
Add redux: 
- ``npm install react-redux``
- ``npm install redux-saga``
- ``npm install redux-devtools-extension``
​
Add a fake REST API in 30 seconds:
- ``npm install json-server``
- create db.json file in root 
- in package.json add ``"dbserver": "json-server --watch db.json --port 8080"``
- when you ``npm start``, now also in another terminal do ``npm run dbserver`` (needs node v10 or higher - use nvm)
- You now have a fake REST api to do CRUD actions with!
​
General process: 
Good to build the skeleton out first, just get one stream working.
E.g. get the READ working out of CRUD first.
- Fill in some data to your db.json
- Hookup an axios call to your db.json
- Hookup store w/ middleware and devtools extension
- Hookup watcher + worker redux actions and redux-saga generator functions
- Use Typescript!
- Write tests as you go, or at least make sure every .ts file has corresponding tests 
- Make sure the whole thing is working, style it, then move onto CREATE, etc. 