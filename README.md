# QuickGPT ⚡

A full-stack AI chat application that supports **text generation** and **AI image generation**, powered by Google Gemini and ImageKit. Users get a credit-based system with paid plans via Stripe, persistent chat history, and a community gallery for published images.

---

## 🚀 Features

- 🤖 **AI Text Chat** — Conversational AI powered by Google Gemini (Gemini Flash model)
- 🎨 **AI Image Generation** — Generate images from text prompts using ImageKit's AI
- 💳 **Credit System** — New users start with 20 free credits (1 credit per text message, 2 per image)
- 💰 **Stripe Payments** — Purchase credit plans (Basic, Pro, Premium) via Stripe Checkout
- 🖼️ **Community Gallery** — Publish generated images to a shared community feed
- 📜 **Chat History** — Persistent, organized chat sessions with full message history
- 🔒 **JWT Authentication** — Secure register/login with bcrypt password hashing
- 📱 **Responsive UI** — Mobile-friendly sidebar with dark-mode gradient design

---

## 🛠️ Tech Stack

### Frontend (`/client`)
| Technology | Purpose |
|---|---|
| React 19 + Vite | UI framework & build tool |
| React Router v7 | Client-side routing |
| Tailwind CSS v4 | Utility-first styling |
| Axios | HTTP client |
| React Markdown + PrismJS | Markdown rendering with code highlighting |
| React Hot Toast | Notifications |
| Moment.js | Timestamp formatting |

### Backend (`/server`)
| Technology | Purpose |
|---|---|
| Node.js + Express 5 | REST API server |
| MongoDB + Mongoose | Database & ODM |
| JWT + bcryptjs | Authentication & password hashing |
| OpenAI SDK (Gemini compatible) | AI text generation |
| ImageKit | AI image generation & media storage |
| Stripe | Payment processing |
| Svix | Stripe webhook verification |

---

## 📋 Credit Plans

| Plan | Price | Credits | Features |
|---|---|---|---|
| **Basic** | $10 | 100 | 100 text + 50 image generations, Standard support |
| **Pro** | $20 | 500 | 500 text + 200 image generations, Priority support |
| **Premium** | $30 | 1000 | 1000 text + 500 image generations, 24/7 VIP support |

---

## 📁 Project Structure

```
QuickGPT/
├── client/                     # React frontend
│   ├── src/
│   │   ├── components/
│   │   │   ├── ChatBox.jsx     # Main chat interface
│   │   │   ├── Message.jsx     # Individual message renderer
│   │   │   └── Sidebar.jsx     # Navigation & chat list
│   │   ├── pages/
│   │   │   ├── Login.jsx       # Auth page (login & register)
│   │   │   ├── Credits.jsx     # Plans & credit purchase
│   │   │   ├── Community.jsx   # Community image gallery
│   │   │   └── Loading.jsx     # Post-payment redirect handler
│   │   ├── context/
│   │   │   └── AppContext.jsx  # Global state (user, chats)
│   │   └── assets/             # Icons, images, prism theme
│   ├── vite.config.js
│   └── vercel.json
│
└── server/                     # Express backend
    ├── configs/
    │   ├── db.js               # MongoDB connection
    │   ├── imageKit.js         # ImageKit SDK setup
    │   └── openai.js           # OpenAI/Gemini client setup
    ├── controllers/
    │   ├── userController.js   # Register, login, profile
    │   ├── chatController.js   # Create & fetch chats
    │   ├── messageController.js# Text & image AI messages
    │   ├── creditController.js # Plans & Stripe checkout
    │   └── webhooks.js         # Stripe webhook handler
    ├── middlewares/            # JWT auth middleware
    ├── models/
    │   ├── User.js             # User schema (name, email, credits)
    │   ├── Chat.js             # Chat & messages schema
    │   └── Transaction.js      # Payment transaction schema
    ├── routes/                 # Express route definitions
    └── server.js               # App entry point
```

---

## ⚙️ Getting Started

### Prerequisites
- Node.js v18+
- MongoDB database (local or [MongoDB Atlas](https://www.mongodb.com/atlas))
- [Stripe](https://stripe.com) account
- [ImageKit](https://imagekit.io) account
- Google Gemini API key

### 1. Clone the repository

```bash
git clone https://github.com/deathstroke2306/QuickGPT.git
cd QuickGPT
```

### 2. Setup the Server

```bash
cd server
npm install
```

Create a `.env` file in the `/server` directory:

```env
PORT=3000
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret_key

# Gemini / OpenAI compatible
OPENAI_API_KEY=your_gemini_api_key
OPENAI_BASE_URL=https://generativelanguage.googleapis.com/v1beta/openai/

# ImageKit
IMAGEKIT_PUBLIC_KEY=your_imagekit_public_key
IMAGEKIT_PRIVATE_KEY=your_imagekit_private_key
IMAGEKIT_URL_ENDPOINT=https://ik.imagekit.io/your_id

# Stripe
STRIPE_SECRET_KEY=your_stripe_secret_key
STRIPE_WEBHOOK_SECRET=your_stripe_webhook_secret
```

Start the server:

```bash
npm run server    # Development (nodemon)
# or
npm start         # Production
```

### 3. Setup the Client

```bash
cd client
npm install
```

Create a `.env` file in the `/client` directory:

```env
VITE_BACKEND_URL=http://localhost:3000
```

Start the development server:

```bash
npm run dev
```

The app will be available at `http://localhost:5173`.

---

## 🌐 API Endpoints

### Auth — `/api/user`
| Method | Endpoint | Description |
|---|---|---|
| POST | `/register` | Register a new user |
| POST | `/login` | Login and receive JWT |
| GET | `/` | Get authenticated user info |
| GET | `/published-images` | Fetch community gallery images |

### Chat — `/api/chat`
| Method | Endpoint | Description |
|---|---|---|
| POST | `/create` | Create a new chat session |
| GET | `/` | Get all chats for the user |

### Messages — `/api/message`
| Method | Endpoint | Description |
|---|---|---|
| POST | `/text` | Send a text message (1 credit) |
| POST | `/image` | Generate an image (2 credits) |

### Credits — `/api/credit`
| Method | Endpoint | Description |
|---|---|---|
| GET | `/plans` | Get all available credit plans |
| POST | `/purchase` | Initiate Stripe checkout for a plan |

### Webhooks
| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/stripe` | Stripe webhook for payment confirmation |

---

## 🚢 Deployment

Both `client` and `server` include a `vercel.json` for easy deployment to [Vercel](https://vercel.com).

1. Deploy the **server** to Vercel and note the production URL.
2. Set `VITE_BACKEND_URL` in the client to point to the server URL.
3. Deploy the **client** to Vercel.
4. Configure your Stripe webhook endpoint to `https://your-server.vercel.app/api/stripe`.

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 🙋‍♂️ Author

**Rishabh Singh**  
GitHub: [@deathstroke2306](https://github.com/deathstroke2306)
