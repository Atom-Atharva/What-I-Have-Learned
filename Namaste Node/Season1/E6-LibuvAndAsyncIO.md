# Libuv and Async IO

Node JS has an event-driven architecture capable of asynchronous I/O.

Since JS is synchronous and single threaded language, it executes the code right away, it does not wait for anything.

## Synchronous and Asynchronous IO

-   In Synchronous IO, system waits till the operation is executed. `(BLOCKING OPERATION)`

-   While in Asynchronous IO, system doesn't wait for the operations to finish, it execute the operations parallel. `(NON-BLOCKING OPERATION)`

-   Example of Synchronous Code:

```js
// JS love this code, Can execute code right away.
var a = 1;
var b = 2;

function multiply(x, y) {
    return x * y;
}

var c = multiply(a, b);
```

-   Example of Async Code:

```js
// These Methods take time to execute.
https.get("YOUR API", (res) => {
    console.log("GOT THE DATA", res.data);
});

fs.readFile("YOUR FILE", "utf8", (data) => {
    console.log("FILE DATA", data);
});

setTimeout(() => {
    console.log("After 5 Seconds");
}, 5000);
```

In V8 JS Engine for synchronous code,there exist a call stack and all the code is wrapped inside `Global Execution Context` and the `variables` are stored inside `heap` and a `garbage collector` is responsible to `clear the heap automatically`, this needs to be done by programmer in low level languages like C/C++.

```
Time, Tide and JS wait for none
```

To make the code async, `Node JS's LIBUV` comes in picture and gives the `Super Powers` to the JS, to execute code in `async ways`.

## Libuv - Super Hero of Node JS

Async IO made `simple`. Just a piece of `C Code`. Libuv act as `middle layer` for V8 Js Engine and OS. Libuv contains `thread pool`, `Event Loop`, etc.

Libuv handles the `async operations` and return the callback function back to `call stack (Main Thread inside V8 Engine)` whenever the data is ready, and code is ready to progress.

![working of Libuv](./assets/Libuv%20and%20Async%20IO.png)

CONCLUSION:

```
JS is synchronous, V8 Engine is synchronous but the Node JS is asynchronous (Non-Blocking IO) because of Libuv.
```
