# 🔥 **What is a Promise?**

A **Promise** in JavaScript represents something that will **happen in the future**.

Example in real life:
"Order placed → Food will come later."

Promise has 3 states:

1️⃣ **pending** (waiting)
2️⃣ **fulfilled** (success)
3️⃣ **rejected** (error)

---

# 🧠 **Why Promises?**

JavaScript is **single-threaded**, so Promises help handle **async tasks** like:

* API Calls
* Database fetch
* File reading
* setTimeout
* Payment verification
* Auth operations

Without blocking the main thread.

---

# ⚙️ **How Promises Work (Very Simple)**

![Image](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/promises.png?utm_source=chatgpt.com)

![Image](https://media.licdn.com/dms/image/v2/D5612AQFANlI5Z3eAGQ/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1672668898515?e=2147483647\&t=gVHhlp8beH3CVWjKM_UI41pKqXLUXLNluR3KsfIHhrI\&v=beta\&utm_source=chatgpt.com)

![Image](https://res.cloudinary.com/dkiurfsjm/image/upload/v1687507931/finally_udjaiz.jpg?utm_source=chatgpt.com)

JavaScript has:

* **Call Stack**
* **Web APIs**
* **Callback Queue**
* **Microtask Queue (for Promises)**
* **Event Loop**

Promise callbacks (`then`, `catch`, `finally`) always go to **Microtask Queue**, which runs **before** normal callbacks.

---

# ✔️ Basic Promise Example

```js
let p = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Done!");
  }, 2000);
});

p.then(result => {
  console.log(result);
});
```

### Flow:

1. Promise created → **pending**
2. After 2 seconds → `resolve("Done!")`
3. `.then()` runs from microtask queue
4. Output: **Done!**

---

# 📌 Promise States

### 1. **Pending**

```js
new Promise(() => {});
```

### 2. **Fulfilled**

```js
resolve("Success");
```

### 3. **Rejected**

```js
reject("Error");
```

---

# 🔁 **Promise Chain (then → then → catch)**

```js
new Promise((res) => res(5))
  .then(x => x * 2)
  .then(y => y + 10)
  .then(final => console.log(final))
  .catch(err => console.log(err));
```

Result:

```
20
```

Each `.then()` receives the previous value.

---

# ❌ **Handling Errors with catch()**

```js
new Promise((resolve, reject) => {
  reject("Something went wrong");
})
.catch(err => console.log(err));
```

Output:

```
Something went wrong
```

---

# 🔄 **finally()**

Runs whether promise succeeds or fails.

```js
p.finally(() => {
  console.log("Execution Completed");
});
```

---

# ⚡ **Promise All, Race, Any, AllSettled**

## 1️⃣ **Promise.all()**

Waits for all promises → returns when all succeed.

```js
Promise.all([p1, p2, p3])
```

If any one fails → the whole thing fails.

---

## 2️⃣ **Promise.race()**

Returns **first completed** promise (success or fail).

```js
Promise.race([p1, p2]);
```

---

## 3️⃣ **Promise.any()**

Returns **first successful** promise.

---

## 4️⃣ **Promise.allSettled()**

Runs all → returns result of each (success + error).

---

# 🔁 **How Promises Work Inside the JavaScript Engine**

![Image](https://media.licdn.com/dms/image/v2/D5612AQHIuZDc3cqPtg/article-cover_image-shrink_600_2000/article-cover_image-shrink_600_2000/0/1721189705579?e=2147483647\&t=7z1ivEBMlIOpeq4P2UUbbrj1T64ysIpkPv27efVvq60\&v=beta\&utm_source=chatgpt.com)

![Image](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/promises.png?utm_source=chatgpt.com)

### Step-by-step:

1. Promise created → executor function runs
2. Async operation (like setTimeout, fetch) goes to **Web APIs**
3. When ready, result goes to **Microtask Queue**
4. Event loop checks:

   * First runs Microtask Queue
   * Then runs Callback Queue
5. `.then()` or `.catch()` executes

This makes Promises **faster** and **prioritized** over callbacks.

---

# 🧩 **Promise vs Callback (Why Promises are better)**

### Callback hell 😭

```js
setTimeout(() => {
  setTimeout(() => {
    setTimeout(() => {
      console.log("Done");
    }, 1000);
  }, 1000);
}, 1000);
```

### Promise chain 😎

```js
doTask()
 .then(step2)
 .then(step3)
 .catch(errorHandler);
```

Cleaner and easier.

---

# 🚀 **Async/Await (Built on Promises)**

Async/await is just a simpler way to write promises.

```js
async function getData() {
  let data = await fetch(url);
  console.log(data);
}
```

---

# 🎯 Summary (Super Easy)

| Feature         | Meaning                      |
| --------------- | ---------------------------- |
| Promise         | Future value holder          |
| States          | pending, fulfilled, rejected |
| then()          | success                      |
| catch()         | error                        |
| finally()       | always runs                  |
| Microtask Queue | priority execution           |
| async/await     | cleaner syntax for promises  |


