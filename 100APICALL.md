# 🔥 **Why does 100 API calls happen?**

Common causes:

1. ❌ **API call written directly inside component body**
2. ❌ **Wrong use of `useEffect` dependencies**
3. ❌ **State updates causing re-renders**
4. ❌ **Typing in search input → making request on every keypress**
5. ❌ **Multiple components calling the same API**
6. ❌ **Using loops to call API inside render**

---

# ✅ **1. MOST IMPORTANT: Use `useEffect` properly**

### ❌ WRONG

(Will cause infinite calls)

```jsx
useEffect(() => {
  fetchData();
});
```

### ✔ RIGHT

(Add dependency `[]` → runs once)

```jsx
useEffect(() => {
  fetchData();
}, []);
```

---

# ✅ **2. Use Debouncing (For search boxes)**

Prevents API from firing on every keystroke.

Install lodash:

```
npm install lodash
```

Usage:

```jsx
import { debounce } from "lodash";

const handleChange = debounce((value) => {
  axios.get(`/search?q=${value}`);
}, 500);
```

✔ Now API fires after user stops typing for 500ms.

---

# ✅ **3. Use Throttling (Limit calls per interval)**

```jsx
const getData = throttle(() => {
  axios.get("/data");
}, 1000);
```

✔ Only 1 call per second.

---

# ✅ **4. Cancel Duplicate Axios Requests**

If a new request comes, cancel the previous one.

```jsx
let controller;

const fetchData = async () => {
  if (controller) controller.abort();
  controller = new AbortController();

  const res = await axios.get("/api/data", {
    signal: controller.signal
  });
};
```

✔ Prevents multiple requests executing simultaneously.

---

# ✅ **5. Use Caching (VERY USEFUL)**

If data already loaded, don’t call API again.

```jsx
const cache = {};

async function fetchUser(id) {
  if (cache[id]) return cache[id];

  const res = await axios.get(`/user/${id}`);
  cache[id] = res.data;

  return res.data;
}
```

✔ Avoid repeat calls.

---

# ✅ **6. Use `useMemo` or `useCallback` to avoid re-calling**

### ❌ WRONG

Function recreated on every render → API may fire repeatedly.

### ✔ Use Memoization

```jsx
const getData = useCallback(() => {
  axios.get("/api");
}, []);
```

---

# ✅ **7. Use React Query (BEST WAY)**

React Query automatically prevents:

✔ Duplicate calls
✔ Infinite calls
✔ Caches response
✔ Deduplicate requests
✔ Refetch control

Example:

```jsx
const { data } = useQuery({
  queryKey: ["todos"],
  queryFn: () => axios.get("/api/todos")
});
```

---

# 🛠 **8. Backend Rate Limiting (Stops spam)**

Install:

```
npm install express-rate-limit
```

Use:

```js
const limiter = rateLimit({
  windowMs: 1 * 60 * 1000,
  max: 100
});

app.use("/api", limiter);
```

✔ Blocks 100+ calls/min per IP.

---

# 🚀 **Best Practices Summary**

| Problem                  | Solution              |
| ------------------------ | --------------------- |
| Multiple calls on mount  | Add `[]` in useEffect |
| Multiple calls on typing | Debounce input        |
| Fast repeated calls      | Throttle              |
| Duplicate calls          | Axios cancel token    |
| Re-render calls          | useMemo, useCallback  |
| Multiple clients         | Backend rate limit    |
| Same data multiple times | Cache it              |
| Complicated states       | Use React Query       |

---

