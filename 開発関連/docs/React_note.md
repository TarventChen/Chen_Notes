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
  } }>
</div>
~~~

# 防止页面刷新

~~~jsx
event.parentDefault();
~~~



​    

# react中的useEffect

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





# 类型注解

~~~tsx
event: React.ChangeEvent<HTMLInputElement>
~~~

- `React.ChangeEvent` 是React库中定义的一种事件对象类型。它表示一个通用的事件对象，可以用于描述各种不同的DOM事件，包括输入元素的变化事件。
- `<HTMLInputElement>` 是一个泛型参数，用于指定事件的目标元素类型。在这种情况下，它指定了事件的目标元素是一个`<input>`元素，通常是表单中的文本输入字段。这个泛型参数有助于提供更具体的类型信息，以便在事件处理函数中使用。

综合起来，`event: React.ChangeEvent<HTMLInputElement>` 告诉你，`event` 参数是一个React定义的事件对象，代表一个`<input>`元素的变化事件，你可以在事件处理函数中使用它来获取有关事件的信息，例如输入元素的值等。

在React中，通常会在事件处理函数中使用这样的类型注解，以确保事件对象被正确类型化，从而避免类型错误，并提供有关事件对象的详细信息。



在许多情况下，不写类型注解或类型声明也可以工作，特别是在TypeScript之外的JavaScript项目中。然而，根据你的具体项目和代码要求，写类型注解或类型声明可以提供以下好处：

1. **类型安全性**：类型注解或声明可以帮助你捕获潜在的类型错误，以确保你正在处理正确类型的数据。这可以在开发过程中减少错误，并提高代码的质量。
2. **代码可读性**：类型注解或声明可以使代码更易于理解。其他开发人员（包括你自己）可以更快地了解事件处理函数的参数类型。
3. **开发工具支持**：如果你使用了带有类型检查的工具（如TypeScript或Flow），类型注解或声明将使这些工具能够提供更好的代码分析和提示。
4. **维护性**：在项目中，特别是在大型项目中，类型信息可以提供文档化的好处，使代码更易于维护和协作。

如果你的项目是一个小型项目或你对类型不太关心，那么可以不写类型注解或声明，而是让JavaScript根据上下文进行类型推断。但在大型项目或需要更多类型安全性的情况下，编写类型注解或声明是一个好的实践，可以提高代码的可维护性和质量。





# enum JavaScriptやTypeScriptのEnum（列挙型

~~~typescript
enum TabType {
  CONTRACT = 0,
  API,
  LIMIT,
}
~~~

これはTabTypeという新しいデータ型を作成し、その中にCONTRACT, API, LIMITという3つの値を割り当てています。それぞれの値は自動的に数字（通常は0から始まる整数）が割り当てられます。したがって、この場合ではCONTRACTは0、APIは1、LIMITは2に対応します。これは特定の状態やタイプの固定リストを持つのに役立ちます。





# Math.ceil()

**`Math.ceil()`** 関数は、引数として与えた数以上の最小の整数を返します。

~~~js
console.log(Math.ceil(0.95));
// Expected output: 1

console.log(Math.ceil(4));
// Expected output: 4

console.log(Math.ceil(7.004));
// Expected output: 8

console.log(Math.ceil(-7.004));
// Expected output: -7

~~~



# useMemo

实现分页使用了两种实现方式

Nomel Way

~~~jsx
<TableBody>
            {!usersQuery.isError &&
            sortedUsers.slice((pageNumber-1)*NumberPerPage, pageNumber * NumberPerPage + NumberPerPage)
            .map((user, index) => {
              return (
                <TableRow
                  key={user.user_number}
                  sx={{
                    'cursor': (user.contractor || user.myself) ? undefined : 'pointer',
                    'backgroundColor': (index % 2 === 0) ? 'secondary.main' : 'secondary.light',
                    '&:hover': {
                      'backgroundColor': '#efeef8',
                    },
                  }}
                  onClick={() => {
                    if (user.contractor || user.myself) return;
                    handleToggleCheck(user.user_number);
                  }}
~~~

useMemo  Way

~~~jsx
// ページング済みカメラ一覧,ページネーション
  const pagedCameras = React.useMemo(() => {
    const start = (pageNumber - 1) * NumberPerPage;
    return sortedCameras.slice(start, start + NumberPerPage);
  }, [sortedCameras, pageNumber]);
~~~

https://zh-hans.react.dev/reference/react/useMemo#usememo

useMemo 它在每次重新渲染的时候能够缓存计算的结果。

~~~jsx	
import { useMemo } from 'react';
function TodoList({ todos, tab }) {
  const visibleTodos = useMemo(
      () => filterTodos(todos, tab),
       [todos, tab]
  );
  // ...
}
~~~

## 参数 

- `calculateValue`：要缓存计算值的函数。它应该是一个没有任何参数的纯函数，并且可以返回任意类型。React 将会在首次渲染时调用该函数；在之后的渲染中，如果 `dependencies` 没有发生变化，React 将直接返回相同值。否则，将会再次调用 `calculateValue` 并返回最新结果，然后缓存该结果以便下次重复使用。
- `dependencies`：所有在 `calculateValue` 函数中使用的响应式变量组成的数组。响应式变量包括 props、state 和所有你直接在组件中定义的变量和函数。如果你在代码检查工具中 [配置了 React](https://zh-hans.react.dev/learn/editor-setup#linting)，它将会确保每一个响应式数据都被正确地定义为依赖项。依赖项数组的长度必须是固定的并且必须写成 `[dep1, dep2, dep3]` 这种形式。React 使用 [`Object.is`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/is) 将每个依赖项与其之前的值进行比较。



## 返回值 

在初次渲染时，`useMemo` 返回不带参数调用 `calculateValue` 的结果。

在接下来的渲染中，如果依赖项没有发生改变，它将返回上次缓存的值；否则将再次调用 `calculateValue`，并返回最新结果。

## Use

你需要给 `useMemo` 传递两样东西：

1. 一个没有任何参数的 calculation 函数，像这样 `() =>`，并且返回任何你想要的计算结果。
2. 一个由包含在你的组件中并在 calculation 中使用的所有值组成的 依赖列表。

在初次渲染时，你从 `useMemo` 得到的 值 将会是你的 calculation 函数执行的结果。

在随后的每一次渲染中，React 将会比较前后两次渲染中的 所有依赖项 是否相同。如果通过 [`Object.is`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/is) 比较所有依赖项都没有发生变化，那么 `useMemo` 将会返回之前已经计算过的那个值。否则，React 将会重新执行 calculation 函数并且返回一个新的值。



### 注意

**你应该仅仅把 `useMemo` 作为性能优化的手段**。如果没有它，你的代码就不能正常工作，那么请先找到潜在的问题并修复它。然后再添加 `useMemo` 以提高性能。







## React.memo 的运行机制

可以在合适的时候使用它来提升性能。

当想要避免子组件不必要的重新渲染（即便父组件发生了更改），你可以使用 `React.memo` 打包子组件 – 只要 props 不发生改变，就不会重复渲染。**请注意此处是引用相等**（译者注：沿用了旧版本 React 的[“浅比较”](https://reactjs.org/docs/shallow-compare.html)）——子组件不会被重新渲染。

```javascript
import { memo } from 'react';

const ChildComponent = (props) => {
  // ...
};

export default memo(ChildComponent);
```
