# React Introduction

* JS library for building user interfaces
    * not a framework
    * it's a small, incomplete solution
    * describes user interface, to display a real user interface
        * declarative, takes care of the how
* design concepts
    * components: describe user interfaces using these
        * simple functions, give input, get output
        * compose bigger components from smaller ones
        * component output is a description of the user interface
        * can contain other components
        * can manage a private state
    * reactive updates
        * when state of component changes, user interface changes as well
    * virtual views in memory
        * write HTML in Javascript
        * using JS to render HTML allows react to have a virtual representation of the DOM in memory
            * virtualDOM
        * tree reconciliation: writes the difference between the new tree and the old tree

## React Components
* state can change
* props are fixed values

### Function Component (stateless)
* receives properties (props), returns JSX (DOM)

### Class Component (stateful)
* receives state and props, returns JSX (DOM)
* can only change internal state, not properties

## Notes
* React cannot return multiple elements in an adjacent way, so when you need sibling elements, you have to wrap them in a parent element
* state of a component can only be accessed by that component, and no one else


## Code Examples

```
// asynchronous way of setting state
this.setState({
    counter: this.state.counter + 1
});

// use if your new state depends on your previous state
this.setState((prevState) => {
    return {
    counter: prevState.counter + 1
};
});
```


Introduction App
```
class Button extends React.Component {
	handleClick = () => {
  	this.props.onClickFunction(this.props.incrementValue);
  }
  
  render() {
  	return (
    	<button onClick={this.handleClick}>
      	+{this.props.incrementValue}
      </button>
    );
  }
}

const Result = (props) => {
	return (
  	<div>{props.counter}</div>
  );
}

class App extends React.Component {
	state = { counter: 0 };
  
  incrementCounter = (incrementValue) => {
  	this.setState((prevState) => ({
    	counter: prevState.counter + incrementValue
    }));
  }
  
	render() {
  	return (
    	<div>
      	<Button onClickFunction={this.incrementCounter} incrementValue={1} />
        <Button onClickFunction={this.incrementCounter} incrementValue={5} />
        <Button onClickFunction={this.incrementCounter} incrementValue={10} />
        <Button onClickFunction={this.incrementCounter} incrementValue={100} />
        <Result counter={this.state.counter}/>
      </div>
    );
  }
}

ReactDOM.render(<App />, mountNode);
```

# Working With Data

## Notes
* determine component structure first
* function components have more benefits than class components, so use them when you can
    * class components should only be used if there's state that needs to be managed (usually top level component) or personalized event handlers
* styling
    * styles.css file -- attributes on elements need to match Javascript DOM api for elements (className vs class) (global)
    * inline Javascript styles `style={{margin: '1em'}}`
* controlled components
    * control element values directly through React rather than reading it from the DOM
* React components have a one way flow of data
    * parent components pass callback functions or primitive values to child components
    * if it's a function, the function can be invoked on the parent from within the child

## Example Code
```
const Card = (props) => {
	return (
  	<div style={{margin: '1em'}}>
    	<img width='75' src={props.avatar_url} />
      <div style={{display: 'inline-block', marginLeft: 10}}>
      	<div style={{fontSize: '1.25em', fontWeight: 'bold'}}>
        	{props.name}
        </div>
        <div>{props.company}</div>
      </div>
    </div>
  );
};

const CardList = (props) => {
	return (
  	<div>
    	{props.cards.map(card => <Card {...card} />)}
    </div>
  );
};

class Form extends React.Component {
	state = { userName: '' };
  
	handleSubmit = (event) => {
  	event.preventDefault();
    axios.get(`https://api.github.com/users/${this.state.userName}`)
    	.then(resp => {
      	this.props.onSubmit(resp.data);
        this.setState({ userName: '' });
      });
  };
  
  render() {
  	return (
    	<form onSubmit={this.handleSubmit}>
      	<input type="text"
        	value={this.state.userName}
          onChange={(event) => this.setState({ userName: event.target.value })} // controlled component
        	placeholder="Github username" required />
        <button type="submit">Add card</button>
      </form>
    );
  }
}

class App extends React.Component {
	state = {
    cards: []
  };
  
  addNewCard = (cardInfo) => {
    this.setState(prevState => ({
    	cards: prevState.cards.concat(cardInfo)
    }));
  }
  
	render() {
  	return (
    	<div>
      	<Form onSubmit={this.addNewCard}/>
        <CardList cards={this.state.cards} />
      </div>
    );
  }
}

ReactDOM.render(<App />, mountNode);
```