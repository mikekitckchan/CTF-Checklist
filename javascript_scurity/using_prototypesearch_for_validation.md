- In Javascript, a function called String.prototype.Search() was normally used to find strings matching with certain words.

- For example, ```js "hello".search(some_input)``` would search for if hello is in the parameter some_input.

- However, the function takes regex of the object instead of string. It would leads to a dot(.) being treated as wildcard. 

- Thus, in some cases in the wild, some programmer would used this for validation in searching certain strings from user input. Attacker can easily bypass by replacing dot(.) in their strings. 
