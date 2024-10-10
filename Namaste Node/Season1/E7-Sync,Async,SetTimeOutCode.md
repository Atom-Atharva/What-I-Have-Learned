# Sync, Async, setTimeoutZero - Code

Here we will understand working of libuv with the help of code.

## Sync Methods

#### File System

```js
fs.readFileSync("./file.txt", "utf8");
```

Reads the content of file `synchronously`, i.e. it will block the main thread while it is running.

### Meaning

V8 Executes the JS code, but `cannot offload` this task to Libuv(which handles async operations).

### Importance

`NOT RECOMMENDED WAY`, but gives you the way to block the main thread using these synchronous methods.

#### Crypto

```js
// pbkdf2 - Password Based Key Derivative Function.
// Used to generate a Cryptographic Key (Synchronously).
crypto.pbkdf2Sync("password", "salt", 50000, 50, "sha512", (err, key) => {
    console.log("KEY IS GENERATED FOR ATOM");
});
```

Crypto is `core module` provided by Node.js, used for `cryptographic operations` like generating secure keys, hashing passwords, etc.

`NOTE:` When the `Sync` is added in the end of function, it means it must be operated Synchronously.

### Meaning

`Blocking Behavior:` The synchronous version of `pbkdf2 (pbkdf2Sync)` will `block` the `event loop`, preventing any other code from executing `until` the key
generation is complete. This can `cause your application` to become `unresponsive` if used inappropriately.

### Alternatives

NodeJs also provides `async versions` of these methods, which offloads the operation to Libuv.

This allows event loop to continue processing tasks while key is been generated.

## Trust Issues with SetTimeout

```js
// Async Code
console.log("Hello from Atom");

var a = 5;
var b = 10;

setTimeout(() => {
    console.log("Log ASAP");
}, 0);

setTimeout(() => {
    console.log("After 10 secs");
}, 10000);

function multiply(x, y) {
    const res = x * y;
    return res;
}

var c = multiply(a, b);

console.log(c);
```

```powershell
# OUTPUT-
Hello from Atom
50
Log ASAP
After 10 secs
```

#### So, why did `setTimeout(0)` executes after multiplication?

-   `Asynchronous Operation:` setTimeout is an asynchronous function, meaning it doesn't block the execution of the code.

-   When you call setTimeout, the callback function is passed to Libuv (Node.js's underlying library), which manages asynchronous operations.

-   `Event Loop and Call Stack:` The callback function from setTimeout(0) is added to the event queue.

-   However, it won't be executed until the current call stack is empty. This means that even if you specify a 0-millisecond delay, the callback will only execute after the global execution context is done.

-   `Trust Issues with setTimeout(0):` When you ask the code to run after 0 milliseconds, it doesn't necessarily run immediately after that time. It runs only when the call stack is empty. This introduces some `"terms and conditions"`, meaning that the actual execution timing is dependent on the state of the call stack.
