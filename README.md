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

