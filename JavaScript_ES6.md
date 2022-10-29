# javascript-interview-questions


## Q.1 How default export behave? rather than normal export

* We can have only one default export in the file.<br>
* If we import inside curley braces that is called named export. If we want to import default export we don't need to define inside the curly braces.<br>
* Named namespace need to give inside curly braces.<br>
* Default export we can define without curley braces.<br>
  <br>
Example (default export):<br>
 
  `import React, {Component} from 'React' ;`

  <br>
  Here, exported file look like;<br>

  `export default React;
  export Component;`


## Q.2 Spread operator uses

* It helps to create array spreading values from another array.
* It's used to create swallow copy for object
* When we use in the method argument we can pass n number of arguments to that function.
* spread oprator always use to last argument of the function.

`let arr1 = [1,2,3];   
let arr2 = [4,5];   
arr1 = [...arr1,...arr2];   
console.log(arr1);`   


> output: [1,2,3,4,5]

`const addNumber = (...args) => { 
  let result = 0;
  args.forEach(ele => result += ele);
  return result;
} 
console.log(addNumber(1,2,3,4,5));`

>output: 15

## Q.3 Object destructuring
* Instead of using dot notation to access the property, we could specify the property name as variable name in the left hand side and assign the object in the right side. 
* Mainly this will be usefull in a function parameter.
- Example,
`let obj = {name: 'john', age:34};
let {name} = obj;
console.log(name);`

>output: john

- Function parameter example,
`let obj = {name: 'john', age:34};
function printName({name}) {
console.log(name);
}
printName(obj);`
