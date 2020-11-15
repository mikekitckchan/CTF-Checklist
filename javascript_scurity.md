## Prototype Pollution

### Introduction
- In Javascript, every objects are collections of key pair. Each pairs are named as properties. For example:

```js
function User(username, password){
    this.username=username;
    this.password=password;
}
```

- In above example, an User is an object and its properties are username and password. To create a new user, can simply input codes as below:

```js
var userA = new User("John", "12345678");

console.log("User "+userA.username + " is created"); //output: User John is created

```

- To change the object properties, we can construction a function to do this. For example, if we want to create a function to change user password, we can make a function like below:

```js
User.prototype.change_password = function(var new_pw){
return this.password=new_pw;
}

userA.change_password("1234"); 

console.log("User "+userA.name+" password now is "+userA.password; //User John passowrd now is 1234
```
- In the above code, a new word prototype came up. Prototype is a property of a function which is also an object itself. In the above code, we have created another property for its prototype called change_password, of which change_password can be used to change User's password. 

### First Exploit using prototype pollution

- Taking the same example, if we create an userB object like below:-

```js

var userB = new User("Sally", "alive");

``` 

- Considering we add one more property to like below:

```js

userB.constructor.prototype.deleted = "yes";

```

- According to the code above, it should affect userB. However, if we print out userA's deleted property, you would find out that it has changed userA as well:

```js
console.log(userA.deleted); //yes
```

### 




