## Prototype Pollution

### Introduction
- In Javascript, every objects are collections of key pair. Each pairs are named as properties. For example:

```js
function Enemy(name, status){
    this.name=name;
    this.status=status
}

var enemyA = new Enemy("John", "Alive");

console.log(enemyA.name + " is " + enemyA.status); //output: John is alive

```
- Apart from this, you can add 

Enemy.prototype.kill = function(){
return this.status;
}

var enenmyA = new Enemy();
enemyA.kill(); //result: enemy is killed

```
- 
