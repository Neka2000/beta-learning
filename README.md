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
