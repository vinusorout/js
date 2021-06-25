Personal learning

# Async Await

```js
// mark the main function async to use await:
const loaddata = async () => {
  const url = "url";
  const res = await fetch(url);
  const data = await res.json();
  return data;
}
loaddata().then(data => console.log(data));

// you cant use await at top-level Await (with out function)
// for this use IIFE, below fuction is IIFE and will execute
( () => {
})();
// async IIFE
( async () => {
  const data = await loaddata();
  console.log(data);
})();

// Top level await is available in Node.js since 14.8
// top-level await is only available in ES modules. (the import statement instead of require)

// first way to ES
// to make a js file as ES script rename the file as .mjs (stands for module JavaScript)
// index.mjs, this top level await will work with command node index.mjs
import got from 'got'; // im mjs file import work not require
const data = await got('url').json();
console.log(data);

// second way to ES
// keep file as index.js, and in package.json file "type": "module"

// Promise.all, let say in index.js with ES
const url2 = "url2";
const url3 = "url3";
const result = await Promise.all([
  fetch(url2),
  fetch(url3)
]);
const dataPromises = results.map(result => result.json())
const finalData = await Promise.all(dataPromises);
console.log(finalData);
```

# Equality
## The == and === is only applicable for primitive types (int, string etc), not for objects for object every language match refrence data
```js
// ==
"1" == 1 // It convert the both side of data in same type before comparison

// ===
"1" === 1 // doesnt convert and result is false

```
