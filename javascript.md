# JavaScript

JavaScript is a coding language that is used to create dynamic web content.
It allows users to interact with websites. 
When loading a webpage, the browser creates a so called **Document Object Model (DOM)**, a tree-like representation of the websites content. 
JavaScript is able to access this **DOM** to change and modify its structure.

### Global Variables
1. the `console` can be used to log information and organize output more generally. The simplest use case is the standard `log()` function: `console.log("Hello, world!");`
3. the `window` object gives access to the current browser window. 
Many of its properties (innerWidth, innerHeight, ...) are global by default.
4. `navigator` provides information about the browser and the environment, such as offline status and preferred user langugage.
5. `setTimeout` and `setInterval` can be used to handle timing-related tasks: 

### Storage Options
JavaScript provides access to various types of storage, that vary in persistence, capacity, access complexity and therefore use cases: 
- **Local Storage** (`localStorage`) is a persistent form of storage (persists even after closing the browser or restarting the device). It stores information per origin (domain + protocol + port).
- **Session Storage** (`sessionStorage`) can be used to store things temporarily. Stored information will not persist when the current tab is closed.
Each tab has its own dedicated session storage.
- Additionally, there are **Cookies** (`document.cookie`) , **Cache Storage** (`caches`) and an indexed database (`indexedDB`), each serving different use cases, such as storing large datasets, tracking and caching.



### Asynchronicity

[`Promises`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) are the main tool used to handle asynchronicity in JavaScript today.  
They are objects representing the eventual completion or failure of an asynchronous operation.  
We can declare asynchronous functions — functions that always return a `Promise` — with the `async` keyword.  
When the function is called, the returned `Promise` will initially be in the *pending* state, and it will eventually either be *fulfilled* or *rejected*.  
To handle promises, there are two main approaches. We will look at them through the example of the [`fetch`](#http-requests) function, as it is a very important and not contrived use case for promises.

#### Async/Await
 The `await` keyword can be used to pause the execution of the surrounding `async` function until the `Promise` settles (Note that a surrounding asynchronous function is needed here!):
```js
async function fetchTasks() {
    try {
        // Send a GET request to '/tasks' (same domain and origin) and wait for the response. 
        // 'response' is a Response object containing metadata like status and headers. The body is not available yet.
        const response = await fetch('/tasks');
        
        // Check for HTTP errors
        if (!response.ok) {
            throw new Error(`HTTP error! Status: ${response.status}`);
        }
        // Read the response body as JSON. This is asynchronous because the body arrives in chunks,
        // so we need to wait until all the data is received before parsing.
        const data = await response.json();
        return data.tasks;
        
    } catch (error) {
        console.error('Fetch failed:', error.message);
        return [];
    }
}
```
A rejected promise results in an error, so we handle the rejected case by catching this error.  
Importantly, **HTTP-level errors (like `404` or `500`) do not cause rejection** — they are considered valid HTTP responses (meaning that we have to handle **HTTP errors** separately), and the promise resolves normally.  

Instead, the promise is only rejected if a **network-level error** occurs, meaning:  
- The request **never reaches the server** (e.g., DNS failure, wrong URL, no internet connection).  
- The request **reaches the server but no response comes back** (e.g., network timeout, connection lost, or manual abortion).  

#### Promise Chaining

Here the same functionality implemented with **Promise Chaining**: 
```js
const tasks = fetch('/tasks')
  .then(response => {
    if (response.ok) {
      return response.json();
    } else {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
  })
  .then(data => data.tasks)
  .catch(error => console.error('Error:', error.message));
```
`.then(results => ..., error => ...)` can be attached to any **Promise**. It takes in two callback functions to handle *fulfilled* and *rejected* promises separately, with the second callback being optional. 
Since `then()` can again (and should in most cases) return a promise, **Promise Chaining** becomes possible (`promise.then(...).then(...).then(...).catch(...)`). `catch()` can handle any error no matter at which link in the chain it occured. Thereby, it provides an alternative to error handling at each step in the chain with the second `then()` callback.

It is also possible to run multiple promises concurrently with various [composition tools](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise#promise_concurrency) (`Promise.all()`, `Promise.any()`, ...).
To create a promise, use the following syntax ([more details here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/Promise#:~:text=See%20also-,Promise()%20constructor,-Baseline%20Widely%20available)): 
```js
new Promise((onFulfilled, onRejected) => ...)
```


### HTTP requests
The globally accessible `fetch()` function is used to make HTTP requests.

### Selecting Elements

To retrieve a single element from the DOM, we can make use of the `id` attribute: 
```js
document.getElementById("myButton");
```
More flexible however, is the `querySelector()` method: 
```js
const button = document.querySelector("#buttonID");
const button = document.querySelector(".buttonClass");
```
It allows us to retrieve the first element that matches a given **CSS selector**, meaning that we can select by class, id, tag, other attributes or nested elements (**#id**, **.class**, ...).

If we want to retrieve all elements that match a certain CSS signature we can instead use the `document.querySelectorAll()` function.


### Further Points
1. Constants and Variables can be defined in the following way: 
```js
let name = "Buddy";  // Can be reassigned
const age = 3;       // Cannot be reassigned
```
2. Compared to Java, JavaScript runs directly in the browser (not in the **JVM**) where it has access to the **DOM**. It has dynamic types and is a **procedural language**, in contrast to Java which is object oriented (an **OOP language**). So it is no longer necessary for code to be within classes, although that is also supported. Code in **procedural languages** is executed from top to bottom, whereas **OOP languages** need a designated entry point (*main()* function)
3. It is possible to dynamically add or remove classes for an element: 
```js
document.querySelector("button").classList.add("active");
```
4. Conversion between JSON (JavaScript Object Notation) and JavaScript objects: 
```js
//String to JS object
const obj = JSON.parse('{"name": "Alice"}'); 

// Object to String: '{"name":"Alice"}'
const str = JSON.stringify(obj);  
```


