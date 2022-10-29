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


