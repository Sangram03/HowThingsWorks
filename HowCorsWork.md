# 🌐 **What is CORS?**

**CORS = Cross-Origin Resource Sharing**

It is a **browser security rule** that decides:

👉 *Can this frontend website call that backend server?*

Example:

```
Frontend: http://localhost:3000
Backend:  http://localhost:5000
```

Different ports = different origins → browser **blocks request** unless backend allows it.

---

# 🧠 **What is an Origin?**

Origin =
`Protocol (http/https) + Domain + Port`

Examples:

| URL                                              | Origin           |
| ------------------------------------------------ | ---------------- |
| [http://localhost:3000](http://localhost:3000)   | origin A         |
| [http://localhost:5000](http://localhost:5000)   | origin B         |
| [https://google.com](https://google.com)         | different origin |
| [https://api.google.com](https://api.google.com) | different origin |

If origins don't match, browser needs **CORS permission**.

---

# ⚠️ Why CORS is Needed?

To stop malicious websites from accessing your backend API without permission.

Without CORS:

* Any random website could call your API
* They could steal tokens, update data, etc.

So browser says:

❌ “Hey backend, should I allow this frontend to talk to you?”

Backend must reply:

✅ “Yes, allow this origin.”

---

# ⚙️ **How CORS Works (Easy Explanation)**

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/0%2Aheiz7awNkQ1B0O8e.png?utm_source=chatgpt.com)

![Image](https://www.keycdn.com/img/support/cors.png?utm_source=chatgpt.com)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AzCXcC1VkBB16BDXUxkWoew.png?utm_source=chatgpt.com)

### Step-by-step:

### 1️⃣ Browser sends request to backend

If request is **simple** (GET, POST with JSON, etc.) → browser checks CORS headers.

### 2️⃣ Backend responds with headers like:

```
Access-Control-Allow-Origin: http://localhost:3000
Access-Control-Allow-Methods: GET,POST
Access-Control-Allow-Headers: Content-Type, Authorization
```

### 3️⃣ Browser reads these headers

If origin matches → request allowed
If not → **blocked**

---

# 🧪 **Preflight Request (OPTIONS)**

When request is **not simple**, browser sends an **OPTIONS** request first.

Example requests that trigger preflight:

* `PUT`, `PATCH`, `DELETE`
* `Content-Type: application/json`
* Requests with **Authorization header**
* Custom headers

### Flow:

```
Browser → OPTIONS Request → Backend → Response with CORS headers → Actual Request
```

---

# 🔥 **CORS Error Example**

If backend does NOT send CORS headers:

```
Access to fetch at "http://localhost:5000/api"
from origin "http://localhost:3000" has been blocked by CORS policy.
```

Browser blocks it.
Backend still receives the request, but browser does not show response.

---

# 🛠 **How to Enable CORS in Node.js (Express)**

```js
const cors = require("cors");
app.use(cors({
    origin: "http://localhost:3000",
    methods: ["GET", "POST", "PUT", "DELETE"],
    credentials: true   // allow cookies / tokens
}));
```

Or allow all:

```js
app.use(cors());
```

---

# 🧩 **How to Enable CORS in Next.js API**

```js
export const corsHeaders = {
  "Access-Control-Allow-Origin": "*",
  "Access-Control-Allow-Methods": "GET, POST, PUT, DELETE",
  "Access-Control-Allow-Headers": "Content-Type, Authorization"
};
```

---

# 📌 **Important Notes**

### ✔ Backend must allow the frontend

CORS is set **on backend**, not frontend.

### ✔ Browser enforces CORS

Postman, mobile apps, backend-to-backend → NOT blocked by CORS.

### ✔ Cookies require special settings

Need:

```
credentials: true
Access-Control-Allow-Credentials: true
Access-Control-Allow-Origin: http://localhost:3000
```

You cannot use `"*"` when sending cookies.

---

# 🎯 Summary (Very Simple)

| Concept       | Meaning                                        |
| ------------- | ---------------------------------------------- |
| CORS          | Allows or blocks frontend from calling backend |
| Origin        | protocol + domain + port                       |
| Preflight     | OPTIONS request before actual request          |
| Allow headers | Backend must respond with permission           |
| Browser       | Only browser blocks due to CORS                |

