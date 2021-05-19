1. function declaration, can use before defining.
```js
function myFunc(){

}
```

2. function expression
```js
myFunc = function(){
    
}
```

3. arrow function
```js
const myFunc = () =>{

}
```

4. define a method in regular way rather than arrow way in an object, as in arrow way you cannot get access to `this`.

5. Hoisting: use a variable before declare.(function declation and var)

6. arrow function does not have argument parameter.

7. closure:

```js
function outer(){
    let param = 1;

    return function inner(){
        param++;
        console.log(param);
    }
}

let myFunc = outer();
myFunc();
myFUnc();
```