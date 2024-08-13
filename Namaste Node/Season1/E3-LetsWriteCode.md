# Lets Write Code

After installing the node in your system, use it with powershell by entering `node`.

Then, you will enter into `NODE REPL (READ, EVALUATE, PRINT, LOOP)`.

Inside Node REPL, we can run JavaScript. Thus, we can say Node is Run Time Environment for JS.

```
Node JS = V8 JS Engine + Super Powers
```

First Program inside Node REPL

```powershell
PS C:\Users\Atharva> node
Welcome to Node.js v18.16.0.
Type ".help" for more information.
> 1+1
2
> 1+1+1+1
4
> var a="Atharva"
undefined
> a
'Atharva'
> var i = 10
undefined
> var j = 20
undefined
> var k = i+j
undefined
> k
30
```

One of the super powers provided by Node JS is `global` object.

Global Object can also be referred as

-   `window` : Inside Browsers
-   `self`
-   `frame`
-   `globalThis` : Standardized Name in all environments.

```js
console.log(global); // Global Object
console.log(this); // Empty Object
console.log(globalThis); // Standard Reference to Global Object
```
