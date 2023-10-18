# Front End Web Development 
This document is intended to cover the aspects required to write front-end production code. It generally follows the format of:
````
//contents section
  //gist cheatsheet link
    //github repo example link
````

Contents: 
- [JavaScript and General knowledge of frontend](#javascript-and-general-knowledge-of-frontend)
- [Algorithms and Data Structures](#algorithms-and-data-structures)
- [Typescript](#typescript)
- [Debugging](#debugging)
- [Devtools and overriding requests](#devtools-and-overriding-requests)
- [React](#react)
- [Redux](#redux)
- [Redux Middleware (redux sagas / thunk) - Depreciated*](#redux-middleware)
- [NPM](#NPM)
- [Webpack](#webpack)
- [Accessibility](#accessibility)
- [TDD](#tdd---test-driven-development)
- [Testing (jest / enzyme / react-testing-library)](#testing---jest--enzyme--react-testing-library)
- [Integration Testing](#integration-testing)
- [Web Performance Optimisation](#web-performance-optimisation)
- [GraphQL](#graphql)
- [Threejs](#threejs)
- [Example of a basic app](#example-of-a-basic-app)
- [Getting a project set up](#getting-a-project-set-up)
- [Notes on an overall quality frontend website](#notes-on-an-overall-quality-frontend-website)


Ideally it would be best to start writing your react application with typescript, redux and TDD from the get-go.
​

Useful guides to know which are the current best languages and frameworks, a collection of tech radars:
- https://kotahi.xero.dev/technology
- https://www.thoughtworks.com/radar/languages-and-frameworks  
- https://www.galaxus.ch/techradar/ 
- https://opensource.zalando.com/tech-radar/
- https://radar.tinkoff.ru/frontend 
​

---
## JavaScript and Frontend Fundamentals
JavaScript is one of the core technologies of the World Wide Web, alongside HTML and CSS. In 2022, 98% of websites use Javascript on the clientside for webpage behavior. 

Notes on understanding JavaScript and frontend fundamentals can be found here: 
- https://github.com/Mark-Cooper-Janssen-Vooles/javascript
- more advanced info is here: https://github.com/Mark-Cooper-Janssen-Vooles/advanced-javascript-concepts


---
## Algorithms and data structures
As seen through the lense of "Big O" notation, these are important to know - as our apps scale the efficiency of the code matters more. Algorithms are also important to know to solve more complex problems and logic. 

- Practice algorithm questions and knowledge here: https://leetcode.com/
- Notes on algorithms and data structures: https://github.com/Mark-Cooper-Janssen-Vooles/js-algorithms-data-structures 

---
## Debugging 
Debugging in JS can be accomplished by two main ways:
1. Using a `console.log()` to log something to the console, which can be accessed in the dev tools of browsers
2. Using the `debugger` keyword, which will open up the dev tools and pause the code at that point. It can then be navigated from there


---
## Devtools and overriding requests
It is recommended to use chrome when developing. Right click a page and click inspect, it will open the dev tools. It will show multiple tabs:
- Elements
  - This tab shows the html elements along with styling and content
    - the sub tab "styles" allows you to see what styles are applied to the selected element and where they are coming from
    - the sub tab "computed" shows the overall affect of styles on the element
    - the sub-tab "accessibility" shows some information on accessibility
- Console
  - this tab is frequently used and shows any errors that may be happening
  - any `console.log()` statements from your app will appear here
  - there are various options to check or uncheck here, such as 'preserve log' which will allow you to compare logs on reload 
- Sources
  - this tab shows you where content is loaded from - i.e the javascript files
  - this is also where the `debugger` will take you to point to the code 
  - you will need to use this to find certain .js files that you wish to override with your local
    - you can use extensions such as `resource override` or `requestly` in chrome to set this up
      - i.e. if your production environment is a URL from `https://www.example.com/business/prod/something/1.2.5/app.js` you can set this to redirect to instead use your local `http://localhost:8080/app.js` to see how your local frontend would work in the prod environment. 
- Network
  - this tab allows you to see network requests for the page you've loaded 
  - it has multiple ways to filter requests, including a searchbar and checkboxes for specific file types (js, css, etc)
  - it also enables you to see the waterfall - what is taking the most time, what is being done async etc 
- Performance 
  - this tab lets you check the web vitals among other things 
- Application
  - this is where things like cookies or local storage is stored temporarily. You can manually delete or add things here 
- Other tabs 
  - You can download extensions and add them here if you wish also - a popular and useful one is Redux for example 


---
## NPM
NPM stands for node package manager and it is a package manage for the JavaScript programming language - the default package manager for the JS runtime environment for node.js.

Notes on understanding NPM can be found here: 
- https://github.com/Mark-Cooper-Janssen-Vooles/understanding_npm


---
## Webpack
Webpack is a static module bundler for javascript applications. It bundles your code together.
- When using webpack, you'll most likely only have one js file and maybe one cs file. no hidden dependencies, and no need to worry about the order of the js files in the html doc anymore. 
- Webpack manages all of your code in one place 

Notes on understanding NPM can be found here: 
- https://github.com/Mark-Cooper-Janssen-Vooles/webpack_learnings


---
## Accessibility
Accessibility (often abbreviated to A11y) means enabling as many people as possible to use Web sites, even when those people's abilities are limited in some way.
- It is possible to get some in-built functionality from 'React Aria': https://react-spectrum.adobe.com/react-aria/
- Certain components prove more difficult than others to make fully accessibile. Check out this for tips: https://www.w3.org/WAI/ARIA/apg/patterns/


https://developer.mozilla.org/en-US/docs/Web/Accessibility

Notes on understanding accessibility can be found here: 
- https://github.com/Mark-Cooper-Janssen-Vooles/accessibility-info 
- Some basics to cover:
  - Browse your website using only keyboard. Tab and Shift + Tab to navigate forwards and backwards, arrow keys to move between options and enter and space to activiate things 
    - Can you interact with every element on the page?
    - Can you see where you are on the page? Look for a visible :focus indicator as you navigate.
    - Can you use functionality (like tooltips) that you usually see on :hover?
    - buttons, links, and form elements get focus automagically. If something's not getting focus, check if it's a div or a span. Check if you can use a different, more semantically appropriate, element.
    - any issues here are critical severity
  - Headings - screen readers use these to navigate around a page
    - Install the Headings [Accessibility Bookmarklet](https://accessibility-bookmarklets.org/install.html) and activate it on your page.
    - Is everything that looks like a heading marked up as a heading?
    - Are the headings nested correctly?
    - Problems here are high severity
  - axe DevTools - it's great at picking up any big accessibility problems (such as form controls missing labels).
    - Install and run [axe Devtools](https://www.deque.com/axe/browser-extensions/) on your page


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

NOTE: Redux-sagas is now depreciated. A 3rd party middleware is not recommended in most cases unless you have complexity. See [here.](https://stackoverflow.com/questions/72360331/is-it-worth-using-redux-saga-in-the-long-term?rq=1#:~:text=Redux%2DSaga%2C%20a%20Redux%20side,and%20no%20longer%20being%20maintained.)

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

When making a failing test pass, commit. You can then refactor if you feel, and commit again. More commits are better.
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

Jest + Enzyme cheatsheet:
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

Notes on typescript with a React + Redux application: 
- https://github.com/Mark-Cooper-Janssen-Vooles/typescript-devs-guide#reactredux--typescript


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
## Web Performance Optimisation
Web performance optimization, or website optimization is the field of knowledge about increasing the speed in which web pages are downloaded and displayed on the user's web browser. 

Notes on understanding performance in frontend development:
- https://github.com/Mark-Cooper-Janssen-Vooles/websiteOptimisation
- [Loading Performance (loading assets)](https://github.com/Mark-Cooper-Janssen-Vooles/websiteOptimisation/blob/master/building-faster-websites.md)
- [Rendering performance (CSS/ js)](https://github.com/Mark-Cooper-Janssen-Vooles/websiteOptimisation/blob/master/CSS-website-performance.md) 
- [React Specific Performance](https://github.com/Mark-Cooper-Janssen-Vooles/websiteOptimisation/blob/master/React-performance-optimisation.md)

---
## GraphQL 
Before there was GraphQL, there was REST.

In recent years, REST has become the dominant API style for building backend web services. With REST, you could signal the type of request we want to make (ex: GET, POST, PUT, or DELETE) and the resource we’d like to fetch or interact with (ex: /api/pets/1) using an HTTP method and a URL.

GraphQL lets you ask for what you want in a single query, saving bandwidth and reducing waterfall requests. It also enables clients to request their own unique data specifications. GraphQL is developed by Facebook.

Website: 
- https://graphql.org/

Notes on understanding GraphQL can be found here: 
- https://github.com/Mark-Cooper-Janssen-Vooles/understanding_graphql

Condensed Gist notes: 
- https://gist.github.com/Mark-Cooper-Janssen-Vooles/bb8b348c7e53b6783caa39ccf67cc6f0


---
## Threejs

Three.js is a 3D JS library that enables devs to create 3D experiences for the web. It works with WebGL, but you can make it work with SVG and CSS but those two are limited.

Notes on threejs:
- https://github.com/Mark-Cooper-Janssen-Vooles/threejs

---
## Example of a basic app
- https://github.com/Mark-Cooper-Janssen-Vooles/quoteApp.UI
​

---
## Getting a project set up 
Get the basic app set up:
- ``npx create-react-app <project-name>``
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

---

## Notes on an overall quality frontend website
There are some things to ask yourself when building quality front end projects. 
- Are you using a well-established library if you have advanced requirements?
  - An example would be React. 
  - Also important is how you've implemented this - building it from scratch can lead to much smaller file sizes than using something like `npx create-react-app`
- Are you implementing typescript for typesafety? 
- Does your pipeline allow you release with confidence? Best practice would be to create scripts for the following to run in the pipeline.
  - Do you have 100% unit test code coverage? (i.e. jest + react testing library)
  - Do you have a few select happy path E2E tests? (i.e. playwright)
  - Do you have optimisation techniques to ensure you don't make the performance worse?
  - Have you considered accessibility and baked it into the project as much as possible (axe unit testing, running audits, manually checking keyboard functionality)