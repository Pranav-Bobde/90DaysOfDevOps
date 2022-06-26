# 25 June 2022 - Day 21

- Run-Time Environment for JS
- Built on Chrome’s V8 JS Engine

### Browser vs Node

![image](https://user-images.githubusercontent.com/66965591/175787385-c45f6ccd-fec9-417b-a853-5d41acde048d.png)


### Global Variables

- As discussed we don’t have window variable in node
- But we got lots of other useful globals
    - To name a few:
    - module - info about the current module
    - require - function to use modules (CommonJS)
    - process - info about the env where the program is being executed

### Modules

- Encapsulated code (only share minimum)
- Node uses CommonJS Library under the hood , Every file is a module (by default)
- To share the data inside your module to the whole app, you need to export it.

```jsx
module.exports = {obj1, func1, var1, ....}
```

#! When you import a module, you actually invoke it.
Node wraps it in the function.

### NPM

`npm test`, `npm start`, `npm restart`, and `npm stop` are all aliases for `npm run xxx.`

For all other `scripts` you define, you need to use the `npm run xxx` syntax.

# 26 June 2022 - Day 22

Bigger Picture

![image](https://user-images.githubusercontent.com/66965591/175835464-ebb5fd6d-341b-40f0-928a-a7fe5212d011.png)

- So in here we have
- V8
    - JS Runtime
- WebAPIs
    - DOM, ajax, setTimeout, etc
- Callback Queue
    - callback functions queue
- Even Loop
    - when stack’s empty pushes the task from the callback queue to the stack

setTimeout is an API provided by the browser. It’s not in the V8. 

### !FUN-FACT

setTimeout() doesn’t guarantee that ur code will run in the given time but after at least the given time.
