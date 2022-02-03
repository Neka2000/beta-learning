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

On objects and arrays you can change the content of a *const* variable, as you can see here:
```
const example = {
    key: 'value'
};
example.key = '123';

const exampleArray = [1];
exampleArray.push(2);
```

Contrary to a *let* variable, a *const* cannot be modified if it's not an object or an array.

- *var*

*var* variables are not block-scoped and can be used globally when declared outside a function. The scope of a variable declared with *var* is its current execution context and closures thereof, which is either the enclosing function and functions declared within it, or, for variables declared outside any function, global. They can also be re-declared and updated.

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

A *var* can also be used before being declared and still works, as you can see here:
```
example = 'test';
var example = 'new test';
```

This is possible because of hoisting, since variable declarations are processed before any code is executed.  

#### Truthy and Falsy values

A truthy value is a value thats considered true when used in a boolean context, and the same applies to a falsy value, but this one is considered false.

Here are some examples of falsy values:

- false
- 0
- -0
- undefined
- null
- ""
- NaN

Every other value is considered truthy, which means they will be considered to be true in a boolean context.

So instead of doing the following:
```
if(array.length > 0){
    return 'example';
}
```

You can simply do:
```
if(array.length){
    return 'example';
}
```

If the array length is 0, it will be false, since 0 is a falsy value.

This can sometimes lead to errors though.
In the following example, we can see a situation where 0 being a falsy value is not desired:
```
const getFlagId = flagId => {
    if(flagId) {
        return 'Flag ID is ${flagId}';
    }
    return 'Flag ID does not exist';
}
```

Here we want to check if the flagId exists, but if the Id is 0, it will not enter the if statement since 0 is a falsy value, even though 0 is a valid flagId.

#### Difference between == and ===

While == compares the operands, not taking into account their types since it transforms the operators to the same type, the === is a strict equality operand, since it also takes into account the type of each operand when comparing them.

This can be seen in the following example:
```
const a = 123;
const b = '123';

if(a == b){
    return 'Using ==';
}
```

This will enter the if condition since a and b have the same value.
But if we use === like so:
```
const a = 123;
const b = '123';

if(a === b){
    return 'Using ==';
}
```

This will not enter the if condition because we are using ===, so even though a and b have the same value, their type is different.

#### Conditional ternary operator

This operator takes three operands:

- A condition, which is followed by a question mark(?);
- An expression that is executed if the previous condition is truthy and is followed by a colon(:);
- And another expression that is executed if the condition is falsy.

Here is an example:
```
const isTrue = true;
const example = isTrue ? 'true' : 'false';
```

The const *example* will take the value 'true', since thats what the conditional ternary operator will return.
Simplified, it's structure should look something like the following:
```
condition ? expressionIfTrue : expressionIfFalse
```

#### Functions and arrow functions

Normal functions and arrow functions work in a very similar way but have some key differences, the most notable one being their syntax.

Example of a normal function:
```
const example = function(arg){
    return true;
}
```

Example of an arrow function with the same behavior:
 ```
const example = (arg) => true;
```

As you can see, arrow functions are shorter and simpler.

Some other differences are:

- Arrow functions do not have arguments binding;
- Arrow functions do not have their own *this*, instead the value of *this* inside an arrow function is bound to the value of *this* of the closest non-arrow parent function;
- Regular functions, unlike arrow functions, are constructible and can be called using the *new* keyword.