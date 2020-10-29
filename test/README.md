# React: Getting Started

React Commonly Faced Problems
> https://jscomplete.com/learn/react-beyond-basics/react-cfp

**Playground**
> https://jscomplete.com/playground

#### React is a JavaScript library (not framework) for building user interfaces

### 3 fundamental concepts of React
1. Components (~ functions), have input and at outbut give you UI
- Function Component (simpler)
- Class Component (more poverful)
2. Reactive updates, no need to worry how to reflect changes in browser, React updates it automatically
3. Virtual views in memory (we use JS to generate HTML)

```javascript
// We get this
<div className = "container">
  <h1>getting Started</h1>
</div>

// using React

React.createElement("div", {className: "container"},
  React.createElement("h1", null, "Getting Started"))
```
Using Playground
```javascript
document.getElementById('mountNode').innerHTML = "Help";
// "Help" will be displayed
```
Example of JSX (commented)
```javascript
// Here is used JSX Extension, it will not be executed simply by browser

function Hellof() {
	// return <div>Hello React!</div>; // JSX line
  // browser is executing this:
  return React.createElement('div', null, 'Hello React!!!');
}

// function to display the text 
ReactDOM.render(
  // <Hellof />, // JSX line
  React.createElement(Hellof, null),
  document.getElementById('mountNode'),
);

// Hello React!!! will be displayes
```
***Create a clicable button***
> Always name your components with uppercase first letter!
```javascript
function Button(){   // don't use lowercase name button - you will get empty button 
  return <button>TEST</button>;
}
ReactDOM.render(
   <Button />,
  document.getElementById('mountNode'),
);
```
Clickable button which shows random number at console after every click
```javascript
// this function is used in onClick attribute
function logRandom(){
  console.log(Math.random());
}

function Button() {
  const [counter, setCounter] = useState(0); // returns an array with 2 elements
  // add onClick attribute
	return <button onClick={logRandom}>{counter}</button>;
}

ReactDOM.render(
  <Button />, 
  document.getElementById('mountNode'),
);

// every time we click buttton - rsndom number is logged in console
```
Double the button's label on each click
```javascript
function Button() {
	const [counter, setCounter] = useState(5);
	return <button onClick={() => setCounter(counter*2)}>{counter}</button>;
}

ReactDOM.render(
  <Button />, 
  document.getElementById('mountNode'),
);
```
Increase value on button by 1 after each click
```javascript
function Button() {
	const [counter, setCounter] = useState(0);
	return <button onClick={() => setCounter(counter+1)}>{counter}</button>;
}

ReactDOM.render(
  <Button />, 
  document.getElementById('mountNode'),
);
```
Multiple buttons which add different values
```javascript
function Button(props) {
  const handleClick = () => props.onClickFunction(props.increment);
	return (
  	<button onClick={handleClick}>
      +{props.increment}
    </button>
  );
}

function Display(props) {
	return (
  	<div>{props.message}</div>
  );
}

function App() {
	const [counter, setCounter] = useState(0);
  const incrementCounter = (incrementValue) => setCounter(counter+incrementValue);
	return (
    <div>
      <Button onClickFunction={incrementCounter} increment={1} />
      <Button onClickFunction={incrementCounter} increment={5} />
      <Button onClickFunction={incrementCounter} increment={10} />
      <Button onClickFunction={incrementCounter} increment={100} />
      <Display message={counter}/>
    </div>  
  );
}

ReactDOM.render(
  <App />, 
  document.getElementById('mountNode'),
);
```
Two examples - using HTML and React for the same task - boxes with texst and real updating time. The HTML version is updating all node every second, while React version - only time, so you are able to type in tha box.<br>
Example in Playground:
> https://jscomplete.com/playground/rgs1.8
```javascript
const render = () => {
  document.getElementById('mountNode').innerHTML = `
    <div>
      Hello HTML
      <input />
      <pre>${(new Date).toLocaleTimeString()}</pre>
    </div>
  `;

  ReactDOM.render(
    React.createElement(
      'div',
      null,
      'Hello React',
      React.createElement('input', null),
      React.createElement('pre', null, (new Date).toLocaleTimeString())
    ),
    document.getElementById('mountNode2')
  );
};

setInterval(render, 1000);
```
### Arrow vs regular functions
```javascript
// REGULAR
const X = function() {
  // "this" here is the caller of X
};

// ARROW
const Y = () => {
  // "this" here is NOT the caller of Y
  // It's the same "this" found in Y's scope
};

/*
  
  Regular functions give access to their "calling" environment while arrow functions give access to their "defining" environment 
  
  
  The value of the "this" keyword inside a regular function depends on HOW the function was CALLED (the OBJECT that made the call).
  
  The value of the "this" keyword inside an arrow function depends on WHERE the function was DEFINED (the SCOPE that defined the function).
  
  */

// console.log(this);

const testerObj = {
  func1: function() {
    console.log('In func1', this);
  },

  func2: () => {
    console.log('In func2', this);
  }
};

testerObj.func1();
testerObj.func2();

// const square1 = (a) => {
// 	return a * a;
// };
// const square2 = (a) => a * a;
// const square3 = a => a * a;

display.log([1, 2, 3, 4].map(a => a * a));
```
### Object literals
```javascript

const mystery = 'answer';
const InverseOfPI = 1 / Math.PI;

const obj = {
	p1: 10,
  p2: 20,
  f1() {},
  f2: () => {},
  [mystery]: 42,
  InverseOfPI,
};

console.log(obj);

// answer: 42
```
### Destructuring
```javascript
// use left variant
const PI = Math.PI;
const E = Math.E;

const {PI, E, SQRT2} = Math;
const SQRT2 = Math.SQRT2;
```
### Template strings
```javascript
const greeting = "Hello World";

const answer = 'Forty Two';

const html = `
  <div>
    ${Math.random()}
  </div>
`;

html
// <div> 0.6067958085817544 </div>
```
### Classes examples
```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
  greet() {
    console.log(`Hello ${this.name}!`);
  }
}

class Student extends Person {
  constructor(name, level) {
    super(name);
    this.level = level;
  }
  greet() {
    console.log(`Hello ${this.name} from ${this.level}`);
  }
}

const o1 = new Person("Max");
const o2 = new Student("Tina", "1st Grade");
const o3 = new Student("Mary", "2nd Grade");
o3.greet = () => console.log('I am special!');

o1.greet(); // Hello Max!
o2.greet(); // Hello Tina from 1st Grade
o3.greet(); // I am special
```
**Randomly change the colour of the text**
```javascript
class ConditionalStyle extends React.Component {
	render() {
  	return (
    	<div style={{ color: Math.random() < 0.5 ? 'green': 'red' }}>
    	  How do you like this?
    	</div>
    );
  }	
}

ReactDOM.render(
	<ConditionalStyle />,
  mountNode,
);
```
