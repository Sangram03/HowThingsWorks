# 🧠 1. **What is TypeScript?**

TypeScript =
**JavaScript + static typing + new features + better tooling**

A browser cannot run TypeScript directly.
So it **compiles to JavaScript**.

```
.ts → ts compiler → .js → browser/node
```

---

# ⚙️ 2. **How TypeScript Works (Internally)**

![Image](https://media.geeksforgeeks.org/wp-content/uploads/20220406145111/TypeScriptCompilation.JPG?utm_source=chatgpt.com)

![Image](https://cdn-media-1.freecodecamp.org/images/1%2AAmv74nfUdirQYlRmSyEMDA.png?utm_source=chatgpt.com)

### Step-by-step:

1. You write `.ts` file
2. `tsc` compiler checks for type errors
3. TS compiles `.ts` → `.js`
4. JavaScript is executed

---

# 🎯 3. **Why TypeScript? (Benefits)**

✔ DetectErrors BEFORE running
✔ Prevent bugs in big MERN apps
✔ Predictable & safe code
✔ Better IntelliSense + autocompletion
✔ Great for team/collaboration
✔ Helps with backend APIs and DB models
✔ Used by Google, Microsoft, Amazon, Netflix

---

# 📦 4. **TypeScript Types (Detailed)**

## **Basic Types**

```ts
let age: number = 20;
let name: string = "Sangram";
let active: boolean = true;
let values: number[] = [1, 2, 3];
```

---

## **Union Types**

Value can be multiple types.

```ts
let id: number | string;
id = 10;
id = "A100";
```

---

## **Literal Types**

```ts
let status: "success" | "error";
```

---

## **Any Type (🚫 Avoid in real apps)**

```ts
let data: any;
```

---

## **Unknown Type** (safer than any)

```ts
let value: unknown;
```

---

## **Void Type**

For functions that return nothing:

```ts
function log(msg: string): void {
  console.log(msg);
}
```

---

## **Never Type**

For functions that never return:

```ts
function error(msg: string): never {
  throw new Error(msg);
}
```

---

# 🧱 5. **Object Types**

```ts
let user: { name: string; age: number };
```

---

# 📘 6. **Interfaces (Very Important)**

Interfaces define **shape of an object**.

```ts
interface User {
  name: string;
  age: number;
  email?: string;  // optional
}
```

Usage:

```ts
const u: User = { name: "Sangram", age: 20 };
```

Interfaces are used everywhere in:

* React props
* API responses
* MongoDB models
* Services

---

# 🪄 7. **Type Aliases**

```ts
type ID = string | number;
type User = { name: string; age: number };
```

---

# 🧠 Interface vs Type — When to Use?

| Feature       | Interface | Type  |
| ------------- | --------- | ----- |
| Extend        | ✔ Yes     | ✔ Yes |
| More readable | ✔ Yes     | 🚫 No |
| Functions     | ✔         | ✔     |
| Unions        | 🚫 No     | ✔ Yes |

**Rule:**

* Use **interface** for objects
* Use **type** for unions and advanced types

---

# 🎛 8. **Generics (MOST IMPORTANT for advanced devs)**

Generics make functions reusable.

```ts
function wrap<T>(value: T): T {
  return value;
}

wrap<string>("hello");
wrap<number>(10);
```

### Generic with interface:

```ts
interface ApiResponse<T> {
  success: boolean;
  data: T;
}
```

---

# 🧩 9. **Classes in TypeScript (with Access Modifiers)**

```ts
class Person {
  constructor(
    public name: string,
    private age: number,
    protected city: string
  ) {}

  getAge() {
    return this.age;
  }
}
```

---

# 🎚 Access Modifiers

| Modifier  | Meaning               |
| --------- | --------------------- |
| public    | accessible everywhere |
| private   | only inside class     |
| protected | class + child classes |

---

# 🧵 10. **Enums**

```ts
enum Role {
  Admin,
  User,
  Guest
}

let r: Role = Role.Admin;
```

---

# 🎯 11. **Tuples**

```ts
let data: [string, number] = ["Sangram", 20];
```

---

# 🔧 12. **Utility Types (Super Important for interviews)**

## **Partial**

```ts
Partial<User>
```

## **Pick**

```ts
Pick<User, "name" | "email">
```

## **Omit**

```ts
Omit<User, "password">
```

## **Readonly**

```ts
Readonly<User>
```

These are heavily used in MERN, Prisma, and Next.js.

---

# 🔥 13. **Type Narrowing (Very useful)**

```ts
function print(val: number | string) {
  if (typeof val === "string") {
    console.log(val.toUpperCase());
  }
}
```

---

# 🧠 14. **Discriminated Unions**

```ts
interface Dog { type: "dog"; bark: () => void }
interface Cat { type: "cat"; meow: () => void }

type Animal = Dog | Cat;

function speak(a: Animal) {
  if (a.type === "dog") a.bark();
}
```

---

# ⚙️ 15. **Modules & Imports**

```ts
import { User } from "./types";
```

---

# 📘 16. **tsconfig.json (Very Important)**

Controls TypeScript behavior.

```json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "commonjs",
    "strict": true,
    "jsx": "react-jsx",
    "outDir": "./dist",
    "baseUrl": "./src"
  },
  "include": ["src"]
}
```

---

# 🔥 17. **TypeScript in React (Important)**

### Typing Props:

```tsx
interface Props {
  name: string;
  count?: number;
}

const Hello: React.FC<Props> = ({ name }) => <h1>{name}</h1>;
```

### Typing useState:

```tsx
const [count, setCount] = useState<number>(0);
```

### Event typing:

```tsx
const handleClick = (e: React.MouseEvent<HTMLButtonElement>) => {};
```

---

# 🧩 18. **TypeScript in Node.js (Backend)**

Express Request/Response typing:

```ts
import { Request, Response } from "express";

const login = (req: Request, res: Response) => {
  res.json({ msg: "Login ok" });
};
```

Typing database models:

```ts
interface User {
  id: string;
  email: string;
  password: string;
}
```

---

# 🔥 19. Advanced TypeScript (for Interviews)

## **Mapped Types**

```ts
type Optional<T> = {
  [K in keyof T]?: T[K];
};
```

## **Infer Keyword**

```ts
type Return<T> = T extends (...args: any[]) => infer R ? R : any;
```

## **Intersection Types**

```ts
type NewType = A & B;
```

## **Index Signatures**

```ts
type Obj = {
  [key: string]: number;
};
```

---

# 🎯 Final Summary (Super Easy)

| Concept       | Meaning              |
| ------------- | -------------------- |
| TypeScript    | JS with types        |
| Compiler      | Converts TS → JS     |
| Interface     | Defines object shape |
| Type          | Alias or union       |
| Generics      | Reusable types       |
| Narrowing     | Detect exact type    |
| Utility types | Powerful shortcuts   |
| TS in React   | Props, state typed   |
| TS in Node    | Strong API typing    |

---
