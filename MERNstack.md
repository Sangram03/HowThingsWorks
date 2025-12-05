# 🌐 **MERN Stack Architecture (High-Level)**

![Image](https://www.bocasay.com/wp-content/uploads/2020/03/MERN-stack-1.png?utm_source=chatgpt.com)

![Image](https://media.geeksforgeeks.org/wp-content/uploads/20231109150525/How-MERN-Stack-Works-copy.webp?utm_source=chatgpt.com)

![Image](https://bezkoder.com/wp-content/uploads/2020/03/react-node-express-mongodb-mern-stack-example-architecture.png?utm_source=chatgpt.com)

```
React (Frontend)
      ↓ API calls (fetch/axios)
Express + Node (Backend)
      ↓
MongoDB (Database)
```

---

# 📦 **Overall Folder Structure**

```
mern-project/
│
├── backend/
│   ├── config/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── middlewares/
│   ├── utils/
│   ├── validations/
│   ├── app.js
│   ├── server.js
│   └── package.json
│
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/ or screens/
│   │   ├── context/ or store/
│   │   ├── hooks/
│   │   ├── utils/
│   │   ├── services/ (api calls)
│   │   ├── assets/
│   │   ├── App.js
│   │   └── index.js
│   └── package.json
│
└── README.md
```

This is the **standard MERN setup**.

---

# 🛠 Backend (Node + Express) Folder Structure (Industry Standard)

![Image](https://miro.medium.com/1%2ACduSgtL14pli4uSWURf19g.jpeg?utm_source=chatgpt.com)

![Image](https://merlino.agency/_next/image?q=75\&url=https%3A%2F%2Fimages.ctfassets.net%2Fvsall43tabcn%2FgyZteBML1XipqwnZTPzRJ%2F0ad14b0e2271d7797e92791b66689ff3%2FClean_Architecture.jpeg\&w=1920\&utm_source=chatgpt.com)

```
backend/
│
├── config/
│    ├── db.js           → MongoDB connection
│    └── env.js          → Env variables load
│
├── models/
│    ├── User.js         → User schema
│    ├── Product.js      → Example schema
│    └── Order.js
│
├── controllers/
│    ├── authController.js
│    ├── userController.js
│    └── productController.js
│
├── routes/
│    ├── authRoutes.js
│    ├── userRoutes.js
│    └── productRoutes.js
│
├── middlewares/
│    ├── authMiddleware.js
│    ├── errorMiddleware.js
│    └── validateMiddleware.js
│
├── validations/
│    ├── userValidation.js
│    └── authValidation.js
│
├── utils/
│    ├── sendEmail.js
│    ├── generateToken.js
│    └── apiResponse.js
│
├── app.js               → Main express setup
├── server.js            → Server start
└── package.json
```

### **Backend Flow (Very Important)**

```
Route → Middleware → Controller → Model → Database → Response
```

Example:

```
/login → validate → authController → User Model → MongoDB → Token
```

---

# 🎨 Frontend (React) Folder Structure

![Image](https://daveceddia.com/images/suggested-structure.png?utm_source=chatgpt.com)

![Image](https://janithl.github.io/images/clean-arch-folders.png?utm_source=chatgpt.com)

```
frontend/
│
├── src/
│   ├── components/    → Reusable UI components
│   ├── pages/         → Page components (Login, Home, Dashboard)
│   ├── layouts/       → Navbar, Sidebar wrappers
│   ├── context/       → Auth context / Global states
│   ├── hooks/         → useAuth, useFetch
│   ├── services/      → API calls (axios)
│   ├── utils/         → helper functions
│   ├── assets/        → Images, icons, CSS
│   ├── App.js
│   └── index.js
```

---

# 📡 API Service Layer (React → Backend)

```
frontend/src/services/api.js
```

Example:

```js
import axios from "axios";

export const api = axios.create({
  baseURL: "https://api.example.com",
  withCredentials: true,
});
```

Per-feature service:

```
services/
 ├── authService.js
 └── productService.js
```

---

# 🧬 Backend Detailed Explanation (Important)

## **1️⃣ models/** → MongoDB Schema

```js
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  password: String,
});
```

---

## **2️⃣ controllers/** → Logic here

Example:

```js
exports.login = async (req, res) => {
  const { email, password } = req.body;
  // login logic
};
```

---

## **3️⃣ routes/** → Endpoints

```js
router.post("/login", login);
```

---

## **4️⃣ middlewares/** → Auth, validation, errors

Example:

```js
module.exports = (req, res, next) => {
  const token = req.headers.authorization?.split(" ")[1];
  if (!token) return res.status(401).json({ message: "Not authorized" });
  next();
};
```

---

## **5️⃣ utils/** → Helpers

Examples:

* sendEmail.js
* token generator
* file upload helper
* response format

---

## **6️⃣ config/** → Environment setup + DB connection

```js
mongoose.connect(process.env.MONGO_URI)
```

---

## **7️⃣ app.js** → Express configuration

```js
app.use(express.json());
app.use(cors());
app.use("/api/auth", authRoutes);
```

---

## **8️⃣ server.js** → Server start

```js
app.listen(5000, () => console.log("Server running"));
```

---

# 🔐 Authentication Folder Structure

```
controllers/authController.js
middlewares/authMiddleware.js
routes/authRoutes.js
utils/generateToken.js
models/User.js
```

---

# 🧪 Example MERN Folder Structure for a Real App

```
mern-project/
│
├── backend/
│   ├── config/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── middlewares/
│   ├── utils/
│   ├── validations/
│   ├── app.js
│   └── server.js
│
└── frontend/
    ├── src/
    │   ├── components/
    │   ├── pages/
    │   ├── context/
    │   ├── services/
    │   └── App.js
```

---

# 🧩 How Data Flows in MERN Stack

![Image](https://www.bocasay.com/wp-content/uploads/2020/03/MERN-stack-1.png?utm_source=chatgpt.com)

![Image](https://bezkoder.com/wp-content/uploads/2020/03/react-node-express-mongodb-mern-stack-example-architecture.png?utm_source=chatgpt.com)

### Example: User registers

```
React (Form)
    ↓ axios
Express Route
    ↓
Controller
    ↓
User Model
    ↓
MongoDB
    ↓
Response to frontend
```

---

# 🎯 Summary (Very Simple)

| Component | What it Contains                 |
| --------- | -------------------------------- |
| React     | UI, components, pages, API calls |
| Express   | Routes, controllers, middlewares |
| Node.js   | Server runtime                   |
| MongoDB   | Database + schemas               |

