# 🔥 **What is TypeScript?**

TypeScript (TS) is a **superset of JavaScript** that adds **static typing**.

```
JavaScript + Types = TypeScript
```

Browser can't run TypeScript directly → it **compiles to JavaScript**.

---

# ⚙️ **How TypeScript Works**

![Image](https://cdn-media-1.freecodecamp.org/images/1%2AAmv74nfUdirQYlRmSyEMDA.png?utm_source=chatgpt.com)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AjfL4pMBAGjrWVRHUQksRDg.png?utm_source=chatgpt.com)

![Image](https://devopedia.org/images/article/165/6445.1554799186.jpg?utm_source=chatgpt.com)

### Flow:

```
TypeScript (.ts/.tsx)
       ↓  tsc compiler
JavaScript (.js)
       ↓
Browser / Node.js executes JS
```

TypeScript catches errors **before running the code**.

---

# 🎯 **Why TypeScript? (Real Benefits)**

✔ Fewer bugs
✔ Predictable code
✔ Auto-suggestions (IDE support)
✔ Type checking
✔ Better documentation
✔ Faster development
✔ Big companies use TS (Google, Microsoft, Meta)

---

# 🧠 **Core TypeScript Concepts**

Let's break them down.

---

# 1️⃣ **Types in TypeScript**

## Basic types:

```ts
let age: number = 20;
let username: string = "Sangram";
let isActive: boolean = true;
let values: number[] = [1, 2, 3];
```

---

# 2️⃣ **Union Types**

```ts
let id: number | string;
id = 10;
id = "A123";
```

---

# 3️⃣ **Type Aliases**

```ts
type UserID = number | string;

let id: UserID = 101;
```

---

# 4️⃣ **Interfaces**

Used to describe object structure.

```ts
interface User {
  name: string;
  age: number;
  active?: boolean;  // optional
}
```

Usage:

```ts
const user: User = {
  name: "Sangram",
  age: 20
};
```

---

# 5️⃣ **Functions with Types**

```ts
function sum(a: number, b: number): number {
  return a + b;
}
```

### Optional params:

```ts
function greet(name?: string) {}
```

---

# 6️⃣ **Generics (VERY important)**

Write reusable components with types.

```ts
function getData<T>(value: T): T {
  return value;
}

getData<string>("hello");
getData<number>(500);
```

---

# 7️⃣ **Enums**

```ts
enum Role {
  Admin,
  User,
  Guest
}

let r: Role = Role.Admin;
```

---

# 8️⃣ **Tuples**

```ts
let user: [string, number] = ["Sangram", 20];
```

---

# 9️⃣ **Classes in TypeScript**

```ts
class Person {
  constructor(public name: string, private age: number) {}

  getAge() {
    return this.age;
  }
}

const p = new Person("Sangram", 20);
```

---

# 🔧 **How TypeScript Helps Frontend (React + TS)**

React components with TypeScript:

```tsx
interface Props {
  name: string;
  count: number;
}

const Hello: React.FC<Props> = ({ name, count }) => {
  return <h1>{name} {count}</h1>;
};
```

### States with type:

```tsx
const [count, setCount] = useState<number>(0);
```

### Event types:

```tsx
const handleClick = (e: React.MouseEvent<HTMLButtonElement>) => {};
```

---

# 💻 **How TypeScript Helps Backend (Node + TS)**

Example Express route:

```ts
import { Request, Response } from "express";

export const login = (req: Request, res: Response) => {
  res.json({ message: "Logged in" });
};
```

### Models:

```ts
interface User {
  id: string;
  email: string;
  password: string;
}
```

---

# 🧩 **tsconfig.json (Very Important)**

This file controls TS behavior.

Example:

```json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "commonjs",
    "strict": true,
    "jsx": "react-jsx",
    "outDir": "./dist"
  },
  "include": ["src"]
}
```

---

# 🚀 **Compile TypeScript → JavaScript**

```
tsc index.ts
```

Output:

```
index.js
```

Or use:

```
npm i -g typescript
npm init -y
tsc --init
```

---

# 🌍 **TypeScript Features Used by Companies**

✔ Types (string, number, boolean)
✔ Optional properties
✔ Interface for API responses
✔ Strong typing for database models
✔ DTOs (Data Transfer Objects)
✔ Generics for reusable code
✔ Utility types: Partial, Required, Pick, Omit
✔ Enum for permission roles
✔ Never, unknown, void

---

# 🔥 **Advanced TypeScript (Useful for Interviews)**

### 1. Utility Types

```ts
type PartialUser = Partial<User>;
type RequiredUser = Required<User>;
type ReadonlyUser = Readonly<User>;
type PickUser = Pick<User, "name" | "email">;
```

---

### 2. Intersection Types

```ts
type A = { name: string }
type B = { age: number }

type C = A & B;   // { name, age }
```

---

### 3. Narrowing

```ts
function print(x: number | string) {
  if (typeof x === "string") {
    console.log(x.toUpperCase());
  }
}
```

---

### 4. Discriminated Unions

```ts
interface Circle {
  type: "circle";
  radius: number;
}
```

---

# 🧠 **How TypeScript Detects Errors BEFORE Running Code**

Example:

```ts
let count: number = "hello"; // ❌ Error
```

TS shows the error **before running** the code → safer.

---

# 🎯 Summary (Super Easy)

| Feature        | Meaning              |
| -------------- | -------------------- |
| Static typing  | Error before runtime |
| Compiles to JS | Browser runs JS      |
| Interfaces     | Object structure     |
| Generics       | Reusable code        |
| TS + React     | Safe UI code         |
| TS + Node      | Stable backend       |
| tsconfig       | Controls compiler    |
| Strong tooling | Better Intellisense  |

---
