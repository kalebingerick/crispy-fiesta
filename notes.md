# React

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