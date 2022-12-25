# javascript-interview-questions


## Q.1 How default export behave? rather than normal export

* We can have only one default export in the file.<br>
* If we import inside curley braces that is called named export. If we want to import default export we don't need to define inside the curly braces.<br>
* Named namespace need to give inside curly braces.<br>
* Default export we can define without curley braces.<br>
  <br>
Example (default export):<br>
 
  ```js
  import React, {Component} from 'React' ;
  ```

  <br>
  Here, exported file look like;<br>

  ```js
  export default React;
  export Component;
  ```


## Q.2 Spread operator uses

* It helps to create array spreading values from another array.
* It's used to create swallow copy for object
* When we use in the method argument we can pass n number of arguments to that function.
* spread oprator always use to last argument of the function.

```js
let arr1 = [1,2,3];   
let arr2 = [4,5];   
arr1 = [...arr1,...arr2];   
console.log(arr1);
```


> output: [1,2,3,4,5]

```js
const addNumber = (...args) => { 
  let result = 0;
  args.forEach(ele => result += ele);
  return result;
} 
console.log(addNumber(1,2,3,4,5));
```

>output: 15

## Q.3 Object destructuring
* Instead of using dot notation to access the property, we could specify the property name as variable name in the left hand side and assign the object in the right side. 
* Mainly this will be usefull in a function parameter.
- Example,
```js
let obj = {name: 'john', age:34};
let {name} = obj;
console.log(name);
```

>output: john

- Function parameter example,
```js
let obj = {name: 'john', age:34};
function printName({name}) {
console.log(name);
}
printName(obj);
```

## Q.4 Advanced features of JavaScript
* Exponential operator *
> \**= this will acting as exponential assignment operator
> x ** y produces the same result as Math.pow(x, y):
```js
let x = 5;
let z = x ** 2;
```

* Array **includes**
> It returns tru or false based on condition which meets
```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];

fruits.includes("Mango");
```
* **padStart** and **padEnd** to support padding at the beginning and at the end of a string.

```js
let text = "5";
text = text.padStart(4,"0");
```

> Result is, 0005 (totally 4 digit takes)

```js
let text = "5";
text = text.padEnd(4,"0");
```

> Result is, 5000 (totally 4 digit takes)

* **Object.entries()** makes it simple to use objects in loops

```ts
const person = {
  firstName : "John",
  lastName : "Doe",
  age : 50,
  eyeColor : "blue"
};

let text = Object.entries(person);
```

> Result like,
> ['firstName', 'John']
> ['lastName', 'Doe']
> ['age', 50]
> ['eyeColor', 'blue']

* **Object.values** it returns the values of object property values as array

```ts
const person = {
  firstName : "John",
  lastName : "Doe",
  age : 50,
  eyeColor : "blue"
};

let text = Object.values(person);
```

> Result will be  ['John', 'Doe', 50, 'blue']

* **async** and **await** its used to handle promises, it will keep on wait for promise result (async request basically).

```js
async function myDisplay() {
  let myPromise = new Promise(function(myResolve, myReject) {
    setTimeout(function() { myResolve("I love You !!"); }, 3000);
  });
  document.getElementById("demo").innerHTML = await myPromise;
}

myDisplay();
```

* JavaScript Object **Rest Properties**

- This allows us to destruct an object and collect the leftovers onto a new object

```js
let { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
x; // 1
y; // 2
z; // { a: 3, b: 4 }
```

* **trimStart()** and **trimEnd()**

> The trimStart()/trimEnd() method works like trim(), but removes whitespace only from the start/end of a string.

* **Object.fromEntries()** 

- The fromEntries() method creates an object from iterable key / value pairs.

```js
const fruits = [
["apples", 300],
["pears", 900],
["bananas", 500]
];

const myObj = Object.fromEntries(fruits);
```

> It generates object. reverse way of Object.entries() function.

### 2020 new features

* **String.matchAll()**

- Before ES2020 there was no string method that could be used to search for all occurrences of a string in a string.

```js
let text = "I love cats. Cats are very easy to love. Cats are very popular."
const iterator = text.matchAll("Cats"); \\ [Cats, Cats]
```

* The Nullish Coalescing Operator **(??)**

- The ?? operator returns the first argument if it is not nullish (null or undefined). Otherwise it returns the second.

```js
let name = null;
let text = "missing";
let result = name ?? text; //result value is missing
```

* The Optional Chaining Operator **(?.)**

-The Optional Chaining Operator returns undefined if an object is undefined or null (instead of throwing an error).

```js
const car = {type:"Fiat", model:"500", color:"white"};
let name = car?.name;
```

* The **&&=** Operator

- The Logical AND Assignment Operator is used between two values. If the first value is true, the second value is assigned.

```js
let x = 10;
x &&= 5; // x =5
```

* The **||=** Operator

- The Logical OR Assignment Operator is used between two values. If the first value is false, the second value is assigned.

```js
let x = 10;
x ||= 5; // x=10

let y = 0;
y||=5; // y=5

### 2021 ES feature

* JavaScript String **ReplaceAll()**

- It will replace all the occurance of the sentances.

```
