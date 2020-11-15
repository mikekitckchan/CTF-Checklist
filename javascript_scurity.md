## Prototype Pollution

### Introduction
- In Javascript, every objects are collections of key pair. Each pairs are named as properties. For example:

```js
function Enemy(name, status){
    this.name=name;
    this.status=status
}
```

- In above example, an Enemy is an object and its properties are name and status.

```js
var enemyA = new Enemy("John", "Alive");

console.log(enemyA.name + " is " + enemyA.status); //output: John is alive

```
- Then we can named the first enemy, enemyA by giving it a name John and status alive. So, this is basically how a Javasript object created. 

- To change the object properties, we can construction a function like below.

```js
Enemy.prototype.kill = function(){
return this.status="dead";
}

enemyA.kill(); //result: enemy is killed
```
- In the above code, a new word prototype came up. Prototype is an mechanism of Javascript's object. 

Prototype pollution is when attacker can find a way to control prototype of the object and change its value to anything they like.


