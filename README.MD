# 🍽️ Food Rescue - Tackling Food Waste with Technology

[![Platform](https://img.shields.io/badge/Platform-Web-blue.svg)](#technology-stack)
[![Backend](https://img.shields.io/badge/Backend-Node.js%20%7C%20Express-green.svg)](#technology-stack)
[![Frontend](https://img.shields.io/badge/Frontend-Next.js%2016%20%7C%20TailwindCSS-brightgreen.svg)](#technology-stack)
[![Database](https://img.shields.io/badge/Database-MongoDB%20%7C%20Mongoose-darkgreen.svg)](#technology-stack)
[![AI Integration](https://img.shields.io/badge/AI%20Model-Llama%203.1%20(Groq)-orange.svg)](#ai-smart-features)

**Food Rescue** is a modern, responsive web application designed to bridge the gap between food donors (restaurants, grocery stores, local food providers, and individuals) and local charities/NGOs (receivers). By leveraging technology, real-time map routing, and smart AI capabilities, the platform streamlines surplus food redistribution—directly reducing greenhouse gas emissions from landfills and helping feed local communities in need.

---

## ✨ Key Features

### 🥦 For Food Donors (Providers)
- **Seamless Listing**: Upload surplus food items quickly with details like food type (Veg, Non-Veg, Mixed), offer type (Donation, Discounted Sale, Community Redistribution), description, and expiry time.
- **📸 Cloudinary Image Uploads**: Add photos of food listings directly to verify quality and freshness.
- **🤖 AI-Generated Copy**: Scribble minimal notes, and our integrated **Llama 3.1 AI** will automatically compose a professional title and detailed description.
- **📊 Personal Impact Dashboard**: Track your total listed food, collected items, estimated meals saved, and total kilograms of food rescued from being wasted.

### 🏠 For Charities & NGOs (Receivers)
- **🔍 Smart Browse & Filtering**: Find food listings filtered by type, keyword search, or distance.
- **📍 Location-Based Recommendations**: Receive smart recommendations sorted by a dynamic priority score that factors in distance, quantity, and impending expiry.
- **🗺️ OSRM Route Planner**: View real-time driving directions, distance (km), and travel duration (minutes) directly from the receiver's location to the donor's pickup point.
- **📦 Claims Management**: Instantly claim food listings, track reservation status, and view historical claims.

### 🔔 Communication & Analytics
- **💬 Real-Time Notification Center**: Receive in-app notifications for claims, status updates, and new nearby listings.
- **✉️ Transactional Emails**: Powered by **Resend**, get notified via email when items are claimed or when a claim status updates.
- **🚨 8km Radius Alerts**: Automated alerts notify nearby charities whenever new food is listed within an 8km radius.
- **📈 Global Impact Stats**: Visualize overall platform performance, including total meals served, total food weight saved, and active donor/receiver user bases.

---

## 🛠️ Technology Stack

### Frontend
- **Framework**: Next.js 16 (React 19, App Router)
- **Styling**: Tailwind CSS v4 & PostCSS
- **Mapping & Routing**: Leaflet, React-Leaflet, and OpenStreetMap
- **Icons**: Lucide React

### Backend
- **Runtime**: Node.js
- **Framework**: Express (v5)
- **Database**: MongoDB (Mongoose ORM)
- **Authentication**: JWT (JSON Web Tokens) with Secure Cookie Session Storage
- **File Uploads**: Multer & Cloudinary SDK

### Third-Party APIs
- **Groq API**: Hosts the `llama-3.1-8b-instant` model for writing listing copy and evaluating priority scores.
- **OSRM (Open Source Routing Machine)**: Computes driving distances and route coordinates.
- **Resend API**: Sends automated transactional email alerts.
- **Cloudinary API**: Stores and serves images for food listings.

---

## 📂 Project Architecture

```
foodrescue-arkajain-hackathon/
├── backend/
│   ├── src/
│   │   ├── config/          # Environment variables & DB connection
│   │   ├── controllers/     # Route logic handlers (auth, food, claim, stats, routes)
│   │   ├── middleware/      # Authentication & Multer upload middleware
│   │   ├── model/           # Mongoose schemas (User, FoodListing, Claim, Notification)
│   │   ├── routes/          # Express API route endpoints
│   │   ├── services/        # Third-party services (Groq AI, Resend Email, Notifications)
│   │   └── app.js           # Core Express configuration
│   ├── server.js            # Node backend entry point
│   └── .env.example
├── frontend/
│   ├── src/
│   │   ├── app/             # Next.js App Router (dashboard, map, claim, recommended, etc.)
│   │   ├── components/      # Shared React components (Navbar, FoodCard, MapClient, etc.)
│   │   ├── context/         # Auth & state providers
│   │   ├── lib/             # API connectivity layer & route helpers
│   │   └── globals.css      # Core styles
│   ├── package.json
│   └── next.config.mjs
└── README.MD                # Workspace documentation
```

---

## 🚀 Setup and Installation

### Prerequisites
- Node.js (v18 or higher)
- MongoDB instance (Local or MongoDB Atlas)
- Accounts/API Keys for:
  - [Cloudinary](https://cloudinary.com/) (For image uploads)
  - [Groq Console](https://console.groq.com/) (For Llama 3.1 AI features)
  - [Resend](https://resend.com/) (For email notifications)

---

### 1. Backend Setup

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Create a `.env` file from the example:
   ```bash
   cp .env.example .env
   ```
4. Configure the following environment variables:
   ```env
   PORT=5000
   JWT_SECRET=your_jwt_secret_key_here
   DATABASE_URL=mongodb+srv://<username>:<password>@cluster.mongodb.net/foodrescue
   FRONTEND_URL=http://localhost:3000
   
   # Cloudinary Configuration
   CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
   CLOUDINARY_API_KEY=your_cloudinary_api_key
   CLOUDINARY_API_SECRET=your_cloudinary_api_secret
   CLOUDINARY_FOLDER=food-rescue
   
   # AI & Email Keys
   GROQ_API_KEY=gsk_your_groq_api_key_here
   RESEND_API_KEY=re_your_resend_api_key_here
   RESEND_FROM_EMAIL=noreply@yourdomain.com
   ```
5. Start the backend server:
   ```bash
   npm start
   ```
   The backend will start running at `http://localhost:5000`. You can visit `http://localhost:5000/api/health` to perform a health check.

---

### 2. Frontend Setup

1. Navigate to the frontend directory:
   ```bash
   cd ../frontend
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Create a `.env.local` file:
   ```bash
   echo "NEXT_PUBLIC_API_URL=http://localhost:5000/api" > .env.local
   ```
4. Start the frontend development server:
   ```bash
   npm run dev
   ```
   Open `http://localhost:3000` in your web browser to access the application.

---

## 🔌 API Endpoints Overview

| Method | Endpoint | Description | Auth Required |
| :--- | :--- | :--- | :--- |
| **POST** | `/api/auth/register` | Register a new provider or receiver | No |
| **POST** | `/api/auth/login` | Login and set session cookie | No |
| **GET** | `/api/auth/get-me` | Get currently logged-in user profile | Yes |
| **POST** | `/api/auth/logout` | Logout and clear session cookies | Yes |
| **POST** | `/api/food/add-food` | Create a new food listing (Supports image file) | Yes (Provider) |
| **POST** | `/api/food/ai-suggest` | Generate copy suggestions via Llama 3.1 | Yes (Provider) |
| **GET** | `/api/food/list` | List all available food items | No |
| **GET** | `/api/food/recommended` | Proximity & urgency recommendations | Yes (Receiver) |
| **POST** | `/api/claim/create-claim/:id`| Claim an available food listing | Yes (Receiver) |
| **GET** | `/api/route/food/:id` | Get OSRM road distance and routing coordinates | Yes |
| **GET** | `/api/stats` | Retrieve platform performance metrics | Yes |
| **GET** | `/api/notifications` | Fetch user alerts & notifications | Yes |

---

## 👥 Team Details

- **Team Name**: **Minion Prince**
- **Team Members**:
  - 👑 **Uday Sawaiyan** (Leader) - [Contact](mailto:udaysawaiyan978@gmail.com)
  - 🧑‍💻 **Aditya Kumar Sharma** - [Contact](mailto:aditya23004@gmial.com)
  - 🧑‍💻 **Aditya Kumar Gupta** - [Portfolio](https://www.devaditya.dev/)
  - 🧑‍💻 **Kunal Kumar Singh** - [Portfolio](https://kunal-dev-topaz.vercel.app/)
  - 👩‍💻 **Sonali Kumari** - [Contact](mailto:sonaliku2904@gmail.com)

---

## 📄 License
This project is licensed under the **ISC License**.
