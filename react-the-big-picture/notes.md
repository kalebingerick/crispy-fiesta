# React: The Big Picture

## History
* created in 2011 by Facebook
* 2012 used on Instagram
* open sourced in 2013
    * markup and logic in a single file
* 2015 open sourced React Native

## Why React?

1. Flexibility
* embeds fewer opinions than Ember or Angular
* library, not framework
    * very flexible because of this
* intended to created components for web apps
    * but can be used for static sites, mobile apps, desktop apps, etc
* renderer is separate from React
    * react dom for web apps
    * react native for react native
    * etc
* awesome-react-renderer
* can convert pages to React in chunks, starting small
* broad browser support bc it's run by Facebook

2. Developer experience
* simple API, easy to learn
    * rarely need to check docs
* JSX that compiles to Javascript
* rather than make HTML more powerful, just write HTML in JS
    * vs fake JS in HTML
* create-react-app
* CodeSandbox

3. Corporate investment
* created and maintained by Facebook
    * facebook.github.io/react/blog
* codemod - command line tool to automate changes (needed to fix breaking changes)
    * automates updating to latest version

4. Community
* huge, active community
    * popularity has steadily grown
    * over 1000 contributors
* Reactiflux
    * online community
* an answer to your question likely exists online
* free component libraries online
    * material-ui
    * react-bootstrap
    * microsoft
    * awesome-react

5. Performance
* Virtual DOM
    * DOM makes JS feel slow
    * updating DOM is expensive, so they needed a more efficient way
        * by minimizing DOM changes
    * compares existing DOM with new DOM, figures out most efficient way to update the DOM
        * avoids layout thrashing (browser has to refigure out where to put everything after DOM changes)
        * saves battery and CPU
        * keeps programming model simple

6. Testability
* friendly to automated testing
* little to no config (create-react-app includes testing configuration)
* test in memory with Node
* reliable, deterministic unit tests that test a single component in isolation
* react components can be pure functions (return value is the same for same arguments, no side effects)
* frameworks
    * mocha, Jasmine, Jest, etc
    * most popular = Jest

## What tradeoffs exist?

1. Framework vs Library
* Angular + Ember are frameworks, React is a library
* Framework
    * contains more opinions, have less options to choose from
    * less setup overhead
    * enforces consistency
* Library
    * light-weight
    * sprinkle it into an app, migrate slowly
    * pick what you need
    * choose best technology
        * Jest/Mocha, Fetch/Axios, etc
    * opinionated popular boilerplates exist

2. Concise vs Explicit
* React trades conciseness for predictability
    * spend more time wiring things together
    * helps people understand what the code is doing
* one-way binding vs two-way binding
    * two-way binding keeps data in sync
    * one-way binding requires an explicit change handler
        * gives you more control

3. Template-centric vs Javascript-centric
* Traditional frameworks
    * make HTML more powerful by allowing you to write JS in HTML
    * `<h1 *ngIf='isAdmin'>Hi Admin</h1>` (angular)
    * `<div v-for'user in users'>{{user.name}}</div>` (vue)
    * less JS knowledge required
    * avoid confusion with JS binding
    * rule of least power: less powerful languages protect from misuse
* React
    * uses power of JS to write HTML
    * `{is Admin && <h1>Hi Admin</h1>`
        * get autocomplete support and error messages
    * `users.map(user => <div>{user.name}</div>)`
    * little framework-specific syntax
    * fewer concepts to learn (it's JS at its core)
    * less code, easier to read
    * encourages improving JS skills

4. Separate Template vs Single File
* MVC popularized separating Model/View/Controller into separate files
    * React components are JS and JSX (single file)
* separation of concerns?
    * Traditional
        * HTML/CSS/JS = separate technologies, but intertwined concerns
        * when changing one file you generally have to change others anyway
    * React
        * Each component is a separate concern
* nested components
    * simple reusable components can be used together to create more complex components

5. Standard vs Non-Standard
* React is a non-standard component library
* Standardized web components
    * four core technologies: templates, custom elements, shadow DOM (encapsulated styling), imports (HTML5 Web Component Fundamentals)
    * yet to be embraced by dev community
    * browser support is spotty
    * does not enable anything new (React can do anything standard web components can)
    * JS libraries keep innovating
    * only runs in the browser (unlike React, which does Desktop apps and VR, etc)
* caniuse

6. Community vs Corporate Backing
* React is backed by Facebook
    * driven by Facebook's needs, so may not be ideal if your needs aren't compatible

## Why not React?

1. HTML and JSX Differ
* 99% the same as HTML
* the differences that do exist are trivial
* what about converting existing HTML?
    * find/replace
    * online compilers
    * npm package that does it for you

2. Build Step Required
* most modern web apps require a build step
    * minifying, transpiling, testing/linting, etc
* Babel and TypeScript both transpile JSX
* `create-react-app`

3. Version Conflicts
* can't run two different versions of React at the same time (because of the runtime)
* standard web components do not require a runtime
* using related libraries requires running compatible versions of those libraries
    * just run a recent version of React
* released codemods easily updates breaking changes

4. Outdated Resources
* tons and tons of resources -- some of which is outdated
* be careful when searching (look at dates)
* multiple features have been extracted from React Core
    * examples
        * `import { render } from 'react-dom'` - react dom is now a new package
        * `create-react-class` is also a new package
        * prop types
        * mixins are now higher order components and render props
* documentation is excellent and actively maintained

5. Decision Fatigue
* React is lightweight and unopinionated, so there's a few ways to do the same thing
* can be good to customize for team needs
* key decisions
    * dev environment
        * andrewhfarmer.com/starter-project
        * can search things you want and things you don't
        * or just start with create-react-app
    * ES Class or createClass
        * `extends React.Component` or `createReactClass`
        * recommends ES class
    * PropTypes, TypeScript, Flow
        * how to handle types
        * prop-types are checked at runtime and during development
        * typescript adds strong typing and compiles to plain Javascript
        * Flow is a static type checker, annotate the top of every file you want it to check
            * runs as a separate process, can be checked whenever
        * recommends prop-types
    * State Management
        * state: app's data
        * popular ways
            * plain react
                * component state
                * handles state well enough, so others are optional
            * flux
                * Facebook's library
                * centralized state
            * redux
                * centralized state
                * immutable data store
            * mobx
                * lighter-weight than redux
                * observable state
                * requires less code, easier to learn
    * Styling
        * start with whatever you know (plain CSS, Sass, Less, etc)
        * Creating Reusable React Components course (by Cory House)

6. ~License~
* Used to have a strict license wrt patents
* MIT open source license

# Questions
* What components can you render on the server? ReactDomServer?
* What are standard web components?