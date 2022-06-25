# 25 June 2022 - Day 13

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
