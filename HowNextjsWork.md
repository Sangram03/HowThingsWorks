# 🚀 **How Next.js Works (Full Explanation)**

Next.js is a **React framework** that provides:

* **Server Side Rendering (SSR)**
* **Static Site Generation (SSG)**
* **API Routes (Backend)**
* **Routing system**
* **Server Components**
* **Client Components**
* **Optimized Bundling**
* **Rendering on the server + browser**

To understand how Next.js works, let’s break it step by step.

---

# 🧠 **1. Next.js = React + Server**

React alone = only runs on **browser**
Next.js = React + **backend server**

So Next.js can run code in:

* **Browser**
* **Node.js server**
* **Edge runtime (Vercel Edge)**

That’s why Next.js apps can have:

* Backend API
* Auth
* Database queries
* SSR pages
* Optimized routing

---

# ⚙️ **2. Next.js Rendering Models**

![Image](https://images.ctfassets.net/9ynx8gh7pmzk/1lUvpi5tc8KzIqdUfPWWfd/38bfce817e76e33a9bf8470d12608aec/image.png?fm=png\&h=589\&q=100\&w=975\&utm_source=chatgpt.com)

![Image](https://h8dxkfmaphn8o0p3.public.blob.vercel-storage.com/learn/dark/learn-client-server-modules.png?utm_source=chatgpt.com)

![Image](https://cdn.sanity.io/images/rdn92ihu/production/17109a56b52f83af20adda513b7f52e01ce803ce-1281x1039.png?auto=format\&fit=max\&h=1039\&w=1281\&utm_source=chatgpt.com)

Next.js provides **multiple ways** to render UI:

---

## **A. CSR – Client Side Rendering (Browser only)**

Like normal React.

Component runs on the browser.

```jsx
"use client";
```

Used for:

* onclick
* useState
* useEffect
* DOM access

---

## **B. SSR – Server Side Rendering**

Runs **before page loads** on server.

```js
export async function getServerSideProps() {}
```

The server runs the code → returns HTML → browser displays.

### Benefits:

* SEO friendly
* Data fresh on every request
* Faster initial paint

---

## **C. SSG – Static Site Generation**

```js
export async function getStaticProps() {}
```

Build time → HTML generated → hosted as static file.

Very fast. Best for blogs, landing pages.

---

## **D. ISR – Incremental Static Regeneration**

Static HTML but updates automatically after a time.

---

# 🔧 **3. Server Components vs Client Components**

Next.js 13+ uses this architecture:

---

## **Server Components**

* Default
* Run on server
* Can fetch data directly
* No bundle sent to browser
* Super fast

Example:

```jsx
// server component by default
export default function Page() {
  const data = await fetch(...);
  return <div>{data}</div>;
}
```

---

## **Client Components**

Required when:

* useState
* useEffect
* event listeners
* localStorage
* window object

Add:

```jsx
"use client";
```

---

# 🌍 **4. Routing in Next.js**

![Image](https://h8dxkfmaphn8o0p3.public.blob.vercel-storage.com/docs/light/terminology-component-tree.png?utm_source=chatgpt.com)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1200/1%2Avq9llllDs4GNS9xq2TWdvg.png?utm_source=chatgpt.com)

![Image](https://i.ytimg.com/vi/GJNlfNKhj6g/hq720.jpg?rs=AOn4CLBPEUmmoS5uUAQdCOZRdYlt7D3Qog\&sqp=-oaymwEhCK4FEIIDSFryq4qpAxMIARUAAAAAGAElAADIQj0AgKJD\&utm_source=chatgpt.com)

Next.js uses **file-based routing**

### Example:

```
app/
  dashboard/
    page.jsx → route: /dashboard
  blog/
    [id]/
      page.jsx → dynamic route: /blog/123
```

No need for react-router.

---

# 🛠 **5. How a Request is Processed in Next.js**

### When user visits `/dashboard`:

```
Browser → Next.js Server → Server Component Fetch Data → 
Build HTML → Send HTML + Cache → Browser shows page →
React hydrates → Client Components activate
```

---

# 🔥 **6. Next.js API Routes (Backend inside Next)**

```
app/api/login/route.js
```

Example:

```js
export async function POST(req) {
  const data = await req.json();
  return Response.json({ success: true });
}
```

This runs **on server only**, never on browser.

You can use:

* MongoDB
* Prisma
* MySQL
* Firebase
* Auth
* Payment gateway

All inside Next.js.

---

# ⚡ **7. Rendering Pipeline**

![Image](https://media2.dev.to/dynamic/image/width%3D800%2Cheight%3D%2Cfit%3Dscale-down%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fxmxoeuxikkb6vw4474aw.png?utm_source=chatgpt.com)

![Image](https://media2.dev.to/dynamic/image/width%3D800%2Cheight%3D%2Cfit%3Dscale-down%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fr4vfvpeikvq39gwuzxal.png?utm_source=chatgpt.com)

![Image](https://images.ctfassets.net/e5382hct74si/kOA2be85nVBQhL0LA9zmO/71f1f53fbf206a18f791b38f8cb2fd6b/Without_React-1.png?utm_source=chatgpt.com)

### Step-by-step:

1. Server components fetch data on server
2. HTML is generated
3. Browser receives HTML
4. Client components are hydrated
5. Page becomes interactive

---

# 🗂 **8. Bundling & Optimization**

Next.js automatically optimizes:

* Images (next/image)
* Fonts
* JS bundling
* Caching
* Prefetching
* Code splitting
* Edge rendering

You don’t need webpack configuration.

---

# 🎯 Summary Table

| Feature       | How it works                           |
| ------------- | -------------------------------------- |
| Rendering     | SSR, CSR, SSG, ISR                     |
| Routing       | File-based (app router)                |
| Components    | Server & Client                        |
| Data fetching | fetch(), API routes, server components |
| Backend       | API routes with Node.js                |
| Performance   | Code splitting, caching, edge runtime  |
| Deployment    | Optimized for Vercel                   |

---
