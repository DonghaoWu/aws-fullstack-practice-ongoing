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

8. constructor function
```js
const Person = function(firstName, lastName){
    this.firstName = firstName;
    this.lastName = lastName;
}

Person.prototype.calAge = function(){
    console.log('age');
}

const me = new Person('hello','world');

console.log(me instanceof Person);
console.log(me.__proto__);
```

9. class
```js
class Person{
    constructor(firstName, lastName){
        this.firstName = firstName;
        this.lastName = lastName;
    }

    calcAge(){
        console.log('hello');
    }

    get firstname(){
        return this.firstName;
    }
}

const me = new Person('hello','world');

console.log(me.firstname)
```

10. static methods.

- a function attatch to constructor, not inheritance
- only used by constrctor
- 
```js
Person.het = function(){
    console.log('hey');
}
```

11. inheritance

```js
const Student = function(fn,ln,course){
    Person.call(this, fn,ln);
    this.course = course;
}

Student.prototype = Object.create(Person.prototype);

Student.prototype.introduce = function(){
    console.log(this.fn);
}
```

12. class inheritance

```js
class Student extends Person{
    constructor(fn,ln,course){
        super(fn, ln);
        this.course = course;
    }
}
```