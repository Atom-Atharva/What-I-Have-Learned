# Diving into NodeJS

Modules works as they are wrapped inside a function when `require("./file.js")` is used and this function is called IIFE.

IIFE (Immediately Invoked Function Expression): Created a function and invoking it immediately.

```js
// Calling a function when declaring it.
(function (module, require) {
    // All Code of Module is wrapped inside this function.
})();

// Module and Require are parameters given by node.
```

Node JS before giving code to V8, it wrap code in IIFE.

Benefits of IIFE:

-   Immediately invokes the code.
-   Privacy: Keeps variables and functions safe.

Node get access to `module.exports` by induced parameter to IIFE.

## 5 Steps Mechanism of `require("./file")`

1. Resolving the Module (Where it is coming from)

    - `./localPath`
    - `.json`
    - `node:module` (Internal Path)

2. Loading the Module (Gets the DATA)

    - File Context is loaded acc to file type.

3. Compile the Module

    - Wraps inside an IIFE.

4. Code Evaluation (Returns for execution)

    - `module.exports`

5. Caching
    - Module is `cached` to increase the efficiency of code by not executing all above steps again.
