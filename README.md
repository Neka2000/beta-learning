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

### The DOM and events

#### The DOM

The DOM is the Document Objet Model of a web page. It is constructed as a tree of Objects that looks like the following:

![DOM Tree of Objects](/images/img_htmltree.gif "HTML Tree of Objects")

Using this model, JavaScript is able to interact with all the HTML elements of a page:
- It can change the HTML element;
- It can change the HTML attributes;
- It can add and remove HTML elements and attributes;
- It can change the CSS styles;
- It can create and react to HTML events.

One of the ways to change the HTML elements of a page is through the *querySelectorAll* method. In the following code we can see an example of this method being used to return all the `<span>` elements of the document:
```
const spans = document.querySelectorAll("span");
```
This will return an array where spans[0] is the first `<span>` element and so on.

Without the DOM, JavaScript wouldn't have a model or notion of web pages, HTML documents and their component parts. All of the elements of the document object model can be accessed and manipulated using the DOM and any scripting language, but in this case we are focusing on JavaScript.

To access the DOM you don't have to do anything special, since you use the API directly in JavaScript from within a script thats run by the browser.

In the following code snippet we can se an example of a function that creates a new `<span>` element, adds content to it and adds it to the document:
```
<html>
    <head>
    <script>

        //Will run the function when the document is loaded
        window.onload = function() {

            //Creates the element
            const span = document.createElement("span");

            //Adds content to the element
            const span_text = document.createTextNode("example");
            span.appendChild(span_text);

            //Adds element to the document
            document.body.appendChild(span);
        }
    </script>
    </head>
    <body>
    </body>
</html>
```

#### Events

Events are actions that happen in the application to which you code can react to.
A simple example is if a user clicks on a button on a webpage, you probably want to react to that action. Thats what events are for.

In the following code snippet we can see an example of a click event:
```
const btn = document.querySelector('button'); //Selecting the button to which the event will be attached

function random(number) {
    return Math.floor(Math.random() * (number + 1));
}

btn.addEventListener('click', () => { //Creates a 'click' event on the button
    const randomColor = `rgb(${random(255)}, ${random(255)}, ${random(255)})`;
    document.body.style.backgroundColor = randomColor;
})
```

This is an example of a click event but there are many other events like `focus`, `mouseover`, `dbclick` and so on.
Events can also be attached to almost any element of a webpage, but there are some events specific to some elements.

## Git

Git is a version control system that tracks the changes in files and allows multiple people to coordinate their work.
### Fundamentals

#### Git Add

`git add` is used to add a file that is in the working directory to the staging area.

#### Git Commit

`git commit` is used to add the staged files to the local repository.

#### Git Push

`git push` is used to add the committed files from the local repository to the remote repository.

#### Git Fetch

`git fetch` is used to get files from the remote repository to the local repository but not into the working directory.

#### Git Merge

`git merge` is used to get the files from the local repository into the working directory.
#### Git Pull

`git pull` is basically a junction of `git fetch` followed by `git merge`. It is used to get files from the remote repository directly into the working directory.

### Advanced Commands

#### Git Branch

`git branch <branch_name>` is used to create a new branch which allows the user to work in parallel to the master branch.

#### Git Checkout

`git checkout <branch_name>` is used to switch the branch the user is working on.

#### Git Rebase

Similar to `git merge`, `git rebase <base>` integrates two branches, with the exception that `git rebase` rewrites the commit history.

#### Git Cherry-Pick

`git cherry-pick <commit_hash>` is used to pick a commit from a branch and apply it to any other branch.
