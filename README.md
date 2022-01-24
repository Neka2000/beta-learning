# BETa Learning
This repository is where I will document and talk about everything I learn throughout the BETa internship.
## Topics
- Javascript
- Git
- React
- Typescript

## Javascript
### Fundamentals

#### Difference between *let*, *const* and *var*

- *let*
*let* is block-scoped and can be updated, but can't be re-declared.

The following code will work:
```
let example = "test";
example = "modified test";
```
The following code will not work:
```
let example = "test";
let example = "modified test";
```
But the following code will work, since the variable is being declared in a different scope:
```
let example = "test";
if(true) {
    let example = "new test";
    console.log(example); //will log "new test"
}
console.log(example); //will log "test"
```
In conclusion, the value of a *let* variable can be modified if needed.

- *const*
Just like *let*, *const* is block scoped and can't be re-declared but it also cannot be updated.

The following code will not work:
```
const example = "test";
example = "modified test";
```
The following code will also not work:
```
const example = "test";
const example = "modified test";
```
Contrary to a *let* variable, a *const* cannot be modified.

- *var*
*var* variables are not block-scoped and can be used globally when declared outside a function. If declared inside a function, it is function-scoped, only being accessible inside that function. They can also be re-declared and updated.

The following code shows a working example:
```
var example = "test";
example = "modified test";
var example = "updated test";
function exampleFunction(){
    var functionVar = "var inside function";
};
console.log(functionVar) //logs an error since the var is not defined
```
