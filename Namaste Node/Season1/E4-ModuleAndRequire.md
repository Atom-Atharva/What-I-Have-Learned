# Module.export and Require

To connect other JS File into existing root file, we use require, so that the code inside the other file will execute directly from the root file.

```js
// xyz.js
console.log("Inside FILE XYZ");
```

```js
// app.js
require("./xyz.js"); // one module into another
console.log("Inside FILE APP");
```

```powershell
# Output
PS D:\Atharva\Coding\Web Development\Node> node app.js
Inside FILE XYZ
Inside FILE APP
```

But, incase of functions and variables

```js
// sum.js
var x = 10;

function calSum(a, b) {
    return a + b;
}
```

```js
// app.js
require("./sum.js");

console.log(x);
console.log(calSum(4, 3));
```

```powershell
# Output
PS D:\Atharva\Coding\Web Development\Node> node app.js
console.log(x);
            ^
ReferenceError: x is not defined
```

This is because module protect their functions and variables from `Leaking`.

Thus we need to export and import variables or functions, use

```js
module.exports = { x, calSum };
```

`NOTE: This type of modules are known as common-js modules(cjs).`

## ES Module (ES6 Module)

This is another way of importing and exporting modules, for using it, just add `package.json` inside repository.

```json
{
    "type": "module"
}
```

Apart from syntax of importing and exporting variable, there is another important difference between cjs and mjs is that the `cjs is synchronous`, and `mjs is asynchronous`.

Also `cjs runs in non-strict mode` and `mjs runs in strict mode`.
