[TOC]



# React start

## Tools

Babel

## import

~~~jsx
import React from "react";
import ReactDOM from "react-dom";

const firstName = "chen";
const lastName = "duo";
const currentDate = new Date().getFullYear();
ReactDOM.render(
  <div>
    <p>Created by {firstName + " " + lastName}</p>
    <p>Copyright {currentDate}</p>
  </div>,
  document.getElementById("root")
);
~~~

## 动态更改react样式

~~~jsx	
//Create a React app from scratch.
//Show a single h1 that says "Good morning" if between midnight and 12PM.
//or "Good Afternoon" if between 12PM and 6PM.
//or "Good evening" if between 6PM and midnight.
//Apply the "heading" style in the styles.css
//Dynamically change the color of the h1 using inline css styles.
//Morning = red, Afternoon = green, Night = blue.

import React from "react";
import ReactDOM from "react-dom";

const time = new Date().getHours();
console.log(time);

const customStyle = {
  color: ""
};

let greeting;
if (time < 12) {
  greeting = "Good Morning";
  customStyle.color = "red";
} else if (time < 18) {
  greeting = "Good Afternoon";
  customStyle.color = "green";
} else {
  greeting = "Good Night";
  customStyle.color = "blue";
}

ReactDOM.render(
  <h1 className="heading" style={customStyle}>
    {greeting}
  </h1>,
  document.getElementById("root")
);

~~~

## es6

Export mutiple things

~~~jsx
export default pi;
export {doublePi, triplePi};
~~~

~~~jsx
import pi, {doublePi, triplePi} from "./math.js";

import * as pi from "./math.js";
~~~



## Local Start

~~~jsx
npx create-react-app my-app
~~~



# React Props

 ~~~jsx
 import React from "react";
 
 function Entry(props) {
   return (
     <div className="term">
       <dt>
         <span className="emoji" role="img" aria-label="Tense Biceps">
           {props.emoji}
         </span>
         <span>{props.name}</span>
       </dt>
       <dd>{props.description}</dd>
     </div>
   );
 }
 
 export default Entry;
 ~~~



# Map

~~~jsx
import React from "react";
import Entry from "./Entry";
import emojipedia from "../emojipedia";

function createEntry(emojiTerm) {
  return (
    <Entry
      key={emojiTerm.id}
      emoji={emojiTerm.emoji}
      name={emojiTerm.name}
      description={emojiTerm.meaning}
    />
  );
}

function App() {
  return (
    <div>
      <h1>
        <span>emojipedia</span>
      </h1>
      <dl className="dictionary">{emojipedia.map(createEntry)}</dl>
    </div>
  );
}

export default App;
~~~



# forEach()

~~~jsx
var newNumbers = [];
numbers.forEach(funcion (x){
	newNumbers.push(x*2);
});
~~~

~~~jsx
const newNumbers = numbers.map(function (x){
    return x*2;
});
~~~



# Filter()

~~~jsx
var numbers = [3, 56, 2, 48, 5];

const newNumbers = numbers.filter(function (num){
    return num > 10;
});

console.log(newNumbers);
~~~

{56, 48}



~~~jsx
var newNumbers = [];
numbers.forEach(function(num){
    if(num < 10){
        newNumbers.push(num);
    }
});
~~~



# reduce()

~~~jsx
var numbers = [3, 56, 2, 48, 5];
var newNumber = numbers.reduce(function(accumulator, currentNumber){
    console.log("accumulator =" + accumulator);
    console.log("currentNumber =" + currentNumber);
    	return accumulator + currentNumber;
})
~~~

~~~html
accumulator = 3
currentNumber = 56
accmu7lator = 59
currentNumber = 2
accumulator = 61
currentNumber = 48
accumulator = 109
currentNumber = 5
~~~



# Ternary Operator



# React Hooks

## State Hooks 

To add state to a component, use one of these Hooks:

- [`useState`](https://react.dev/reference/react/useState) declares a state variable that you can update directly.
- [`useReducer`](https://react.dev/reference/react/useReducer) declares a state variable with the update logic inside a [reducer function.](https://react.dev/learn/extracting-state-logic-into-a-reducer)

~~~jsx
import React, { useState } from "react";

function App() {
  const [count, setCount] = useState(0);
	//count代表初始状态， setCount设置状态
  function increase() {
    setCount(count + 1);
  }

  function decrease() {
    setCount(count - 1);
  }
  
  return (
    <div className="container">
      <h1>{count}</h1>
      <button onClick={increase}>+</button>
      <button onClick={decrease}>-</button>
    </div>
  );
}

export default App;
~~~

# 解构赋值 Destructuring

~~~js
import cars from "./practice";
import ReactDOM from "react-dom";
import React from "react";

const [honda,tesla] = cars;

const {
  speedStats: { topSpeed: hondaTopSpeed }
} = honda;

const {
  speedStats: { topSpeed: teslaTopSpeed }
} = tesla;

const {coloursByPopularity : [hondaTopColour]} = honda;
const {coloursByPopularity : [teslaTopColour]} = tesla;

ReactDOM.render(
  <table>
    <tr>
      <th>Brand</th>
      <th>Top Speed</th>
    </tr>
    <tr>
      <td>{tesla.model}</td>
      <td>{teslaTopSpeed}</td>
      <td>{teslaTopColour}</td>
    </tr>
    <tr>
      <td>{honda.model}</td>
      <td>{hondaTopSpeed}</td>
      <td>{hondaTopColour}</td>
    </tr>
  </table>,
  document.getElementById("root")
);
~~~



# Class Components vs Functional Components

## Functional Components

~~~jsx

import React, { useState } from "react";
  
const FunctionalComponent = () => {
    const [count, setCount] = useState(0);
  
    const increase = () => {
        setCount(count + 1);
    }
  
    return (
        <div style={{ margin: '50px' }}>
            <h1>Welcome to Geeks for Geeks </h1>
            <h3>Counter App using Functional Component : </h3>
            <h2>{count}</h2>
            <button onClick={increase}>Add</button>
        </div>
    )
}
  
export default FunctionalComponent;
~~~



## Class Components

~~~jsx
import React, { Component } from "react";
  
class ClassComponent extends React.Component {
    constructor() {
        super();
        this.state = {
            count: 0
        };
        this.increase = this.increase.bind(this);
    }
  
    increase() {
        this.setState({ count: this.state.count + 1 });
    }
  
    render() {
        return (
            <div style={{ margin: '50px' }}>
                <h1>Welcome to Geeks for Geeks </h1>
                <h3>Counter App using Class Component : </h3>
                <h2> {this.state.count}</h2>
                <button onClick={this.increase}> Add</button>
  
            </div>
        )
    }
}
  
export default ClassComponent;
~~~



# React Forms

~~~jsx
import React, { useState } from "react";

function App() {
  const [fName, setFname] = useState("");
  const [lName, setLname] = useState("");

  function handleFChange(event) {
    const firstName = event.target.value;
    setFname(firstName);
  }
  function handleLChange(event) { 
    const lastName = event.target.value;
    setLname(lastName);
  }
  return (
    <div className="container">
      <h1>
        Hello {fName} {lName}
      </h1>
      <form>
        <input
          onChange={handleFChange}
          name="fName"
          placeholder="First Name"
          value={fName}
        />
        <input
          onChange={handleLChange}
          name="lName"
          placeholder="Last Name"
          vale={lName}
        />
        <button>Submit</button>
      </form>
    </div>
  );
}

export default App;
~~~

- event.target.value

这个名为 `handleLChange` 的函数是在 `onChange` 事件触发时执行的代码。参数 `event` 是一个事件对象，通过它可以获取到事件发生在哪个元素上，以及该元素的值等信息。

`event.target` 指的是触发事件的元素。在这个例子中，事件是由输入字段（`<input>`）触发的。因此，`event.target.value` 表示当前输入字段的值（文本）。这个值就是用户输入的文本。

# Complex State

~~~jsx
mport React, { useState } from "react";

function App() {
  const [fullName, setFullname] = useState({
    fName: "",
    lName: ""
  });
  

  function handle(event) {
    const newValue = event.target.value;
    const inputName = event.target.name;

    setFullname(prevValue => {
      if(inputName === "fName"){
        return{
          fName: newValue,
          lName: prevValue.lName
        }
      }else if(inputName === "lName"){
        return{
          fName: prevValue.fName,
          lName: newValue
        }
      }
    });
}

  return (
    <div className="container">
      <h1>
        Hello {fullName.fName} {fullName.lName}
      </h1>
      <form>
        <input
          onChange={handle}
          name="fName"
          placeholder="First Name"
          value={fullName.fName}
        />
        <input
          onChange={handle}
          name="lName"
          placeholder="Last Name"
          vale={fullName.lName}
        />
        <button>Submit</button>
      </form>
    </div>
  );
}

export default App;
~~~



~~~jsx
import React, { useState } from "react";

function App() {
  const [contact, setContact] = useState({
    fName: "",
    lName: "",
    email: ""
  });
  
  function handle(event){
    const newValue = event.target.value;
    const input = event.target.name;
    
    setContact(prevValue => {
      if(input === "fName"){
        return{
            fName: newValue,
            lName: prevValue.lName,
            email: prevValue.email
          }
      }else if(input === "lName"){
        return{
          fName: prevValue.fName,
          lName: newValue,
          email: prevValue.email
        }
      }else if(input === "email"){
        return{
          fName: prevValue.fName,
          lName: prevValue.lName,
          email: newValue
        }
      }
    });
  }


  return (
    <div className="container">
      <h1>
        Hello {contact.fName} {contact.lName}
      </h1>
      <p>{contact.email}</p>
      <form>
        <input name="fName" placeholder="First Name" onChange={handle} value={contact.fName}/>
        <input name="lName" placeholder="Last Name" onChange={handle} value={contact.lName}/>
        <input name="email" placeholder="Email" onChange={handle} value={contact.email}/>
        <button>Submit</button>
      </form>
    </div>
  );
}

export default App;

~~~



# ES6 Spread Operator

~~~jsx
const citrus = ["Lime", "Lemon", "Orange"];
const fruits = ["Apple", ...citrus, "Banana", "Cocnut"];

console----
["Apple","Lime", "Lemon", "Orange","Banana", "Cocnut"]
~~~

## VS

- without Spread Operator

~~~jsx
const fullName = {
  fName: "James",
  lName: "Bond"
}

const user = {
  fullName,
  id: 1,
  username: "jamesbond007"
}

console.log(user);
~~~

~~~html
fullName: Object
fName: "James"
lName: "Bond"
id: 1
username: "jamesbond007"
~~~

- Use Spread Operator

  ~~~jsx	
  const fullName = {
    fName: "James",
    lName: "Bond"
  }
  
  const user = {
    ...fullName,
    id: 1,
    username: "jamesbond007"
  }
  
  console.log(user);
  ~~~

  ~~~html
  fName: "James"
  lName: "Bond"
  id: 1
  username: "jamesbond007"
  ~~~




# Managing  a Component Tree

~~~~jsx
<div onClick={props.onChecked(props.id)}>

</div>
~~~~



~~~jsx
<div onClick={() =>{
        props.onChecked(props.id);
  } }
    </div>
~~~

# 防止页面刷新

~~~jsx
event.parentDefault();
~~~



​    

# react中的useEffect

[![img](https://cdn2.jianshu.io/assets/default_avatar/7-0993d41a595d6ab6ef17b19496eb2f21.jpg

是函数组件中执行的副作用，副作用就是指每次组件更新都会执行的函数，可以用来取代生命周期。

### 1. 基本用法



```js
import { useEffect } from "react";
useEffect(()=>{
    console.log('副作用');   
});
```

### 2. 副作用分为需要清除的和不需要清除

假如设置一个定时器，当组件卸载时需要将定时器关闭，这就是需要清除的。

需要清除的需要在副作用中返回一个函数即可，返回的函数编写需要的代码逻辑。



```js
import { useEffect } from "react";
useEffect(()=>{
    return () => {
        console.log('执行代码逻辑');
    }
});
```

不需要清除的就是正常的。

### 3. 传入第二个参数

- 不传入，则组件更新时就会执行。
- 传入空数组[]

则代表只运行一次(仅在组件挂载和卸载时执行),当副作用没有返回函数时可以当做生命周期`componentDidMount`使用，返回函数时可以当做生命周期`componentWillUnmount`使用

```js
// 当做 componentDidMount使用
import { useEffect } from "react";
useEffect(()=>{
    console.log('页面渲染完成');
}, []);
```

```js
// 当做 componentWillUnmount使用
import { useEffect } from "react";
useEffect(()=>{
    return () => {
        console.log('组件卸载');
    }
}, []);
```

- 传入数组 [item]

```js
import { useEffect, useState } from "react";
const [ count, setCount ] = useEffect(1);
useEffect(()=>{
    console.log('执行了');
}, [count]);
```

当数组不为空时，组件更新时，会检测`count`的值，若更新后的值与旧值不一样则会调用`effect`，若相同则会跳过执行。

若数组传入多个参数，只要有一项有变更就会执行`effect`。



# 解构

~~~JSX
const [showLogout, setShowLogout] = useState(false);
~~~

这里 `useState(false)` 返回一个包含两个元素的数组，第一个元素是状态变量 `showLogout`，第二个元素是用于更新状态的函数 `setShowLogout`。通过数组解构，你将这两个元素分别赋值给了 `showLogout` 和 `setShowLogout`。

~~~JSX
const { user, logoutUser } = useDashboardContext();
~~~

这里假定 `useDashboardContext()` 返回一个包含 `user` 和 `logoutUser` 属性的对象。通过对象解构，你将对象中的这两个属性分别赋值给了 `user` 和 `logoutUser`。

