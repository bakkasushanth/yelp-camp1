# 🏕️ YelpCamp — Campground Review Platform

![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Express.js](https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white)
![EJS](https://img.shields.io/badge/EJS-B4CA65?style=for-the-badge&logo=ejs&logoColor=black)
![Passport.js](https://img.shields.io/badge/Passport.js-34E27A?style=for-the-badge&logo=passport&logoColor=white)
![Cloudinary](https://img.shields.io/badge/Cloudinary-3448C5?style=for-the-badge&logo=cloudinary&logoColor=white)

> A full-stack campground review web application built with the MEN stack. Features user authentication, campground CRUD, multi-image uploads, interactive Mapbox maps, and a review system — with security hardened via Helmet, Joi validation, and input sanitization.

🔗 **[Live Demo](https://YOUR_RENDER_LINK_HERE)** &nbsp;|&nbsp; 📄 **[My Resume]()**

---

## 📸 Screenshots

> *(Add screenshots here after deploying — drag and drop images directly into the GitHub README editor)*

---

## ✨ Features

- 🔐 **Passport.js Authentication** — Secure register/login with hashed passwords via passport-local-mongoose
- 🏕️ **Campground CRUD** — Create, view, edit, and delete campgrounds with full author-only authorization
- ⭐ **Reviews & Ratings** — Authenticated users can post and delete reviews on any campground
- 🗺️ **Interactive Maps** — Mapbox cluster map on index page + per-campground location pin via @mapbox/mapbox-sdk & @maptiler/client
- 🖼️ **Image Uploads** — Multi-image upload per campground stored on Cloudinary CDN via Multer
- 🔒 **Security** — Helmet.js HTTP headers, express-mongo-sanitize (NoSQL injection), sanitize-html (XSS), Joi server-side validation
- 💬 **Flash Messages** — Contextual success/error feedback using connect-flash
- 📱 **Fully Responsive** — Works seamlessly on mobile, tablet, and desktop
- 🗃️ **Persistent Sessions** — Sessions stored in MongoDB via connect-mongo (survive server restarts)

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | EJS, EJS-Mate (layouts), Bootstrap 5 |
| Backend | Node.js, Express.js |
| Database | MongoDB, Mongoose |
| Auth | Passport.js, passport-local, passport-local-mongoose |
| Maps | Mapbox SDK, MapTiler Client |
| Storage | Cloudinary, Multer, multer-storage-cloudinary |
| Security | Helmet, express-mongo-sanitize, sanitize-html, Joi |
| Dev Tools | dotenv, nodemon, method-override, connect-flash |

---

## 📁 Project Structure

```
yelp-camp/
├── cloudinary/             # Cloudinary config & multer storage setup
├── controllers/            # Route logic (campgrounds, reviews, users)
├── middleware.js           # Auth & validation middleware
├── models/                 # Mongoose schemas (User, Campground, Review)
├── public/                 # Static assets (CSS, JS, images)
├── routes/                 # Express routers (campgrounds, reviews, users)
├── seeds/                  # DB seed data
├── utils/                  # ExpressError & catchAsync helpers
├── views/                  # EJS templates
│   ├── campgrounds/        # Index, show, new, edit views
│   ├── layouts/            # EJS-Mate boilerplate layout
│   ├── partials/           # Navbar, flash messages
│   └── users/              # Login & register views
├── app.js                  # Express app entry point
├── .env.example
└── package.json
```

---

## ⚙️ Local Setup

### Prerequisites
- Node.js v18+
- MongoDB (local or [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) free tier)
- Cloudinary account (free tier)
- Mapbox account (free tier)
- Git

### 1. Clone the repo
```bash
git clone https://github.com/bakkasushanth/yelp-camp1.git
cd yelp-camp1/yelp-camp
```

### 2. Setup environment variables
Create a `.env` file in the `yelp-camp/` folder:
```env
CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_KEY=your_cloudinary_api_key
CLOUDINARY_SECRET=your_cloudinary_api_secret
MAPBOX_TOKEN=your_mapbox_access_token
DB_URL=your_mongodb_connection_string
SECRET=your_session_secret
```

### 3. Install dependencies
```bash
npm install
```

### 4. Seed the database (optional)
```bash
node seeds/index.js
```

### 5. Run the app
```bash
npm start
```

App runs at **http://localhost:3000**

---

## 🚀 Deploy on Render (Free)

> Follow these steps to get a live demo link to put on your resume

### Web Service
1. Go to [render.com](https://render.com) → **New** → **Web Service**
2. Connect your GitHub → select `yelp-camp1`
3. Set:
   - **Root Directory:** `yelp-camp`
   - **Build Command:** `npm install`
   - **Start Command:** `node app.js`
4. Add all environment variables from your `.env` file
5. Click **Deploy** — you'll get a URL like `https://yelpcamp.onrender.com`

**Paste that URL in the Live Demo badge at the top of this README.**

---

## 🔒 Security Implementation

| Threat | Solution |
|---|---|
| NoSQL Injection | express-mongo-sanitize |
| XSS Attacks | sanitize-html + Helmet CSP headers |
| Schema Validation | Joi server-side validation |
| Password Storage | passport-local-mongoose (pbkdf2 hashing) |
| Insecure HTTP Headers | Helmet.js (14 middleware headers) |
| Session Hijacking | Secure session secret + connect-mongo |

---

## 📊 Performance Metrics

| Metric | Result |
|---|---|
| Image Storage | Cloudinary CDN (optimised delivery) |
| Session Persistence | MongoDB-backed sessions (connect-mongo) |
| Map Rendering | Mapbox GL cluster map (lazy-loads markers) |
| Auth | Passport.js + pbkdf2 (zero plain-text passwords) |

---

## 🤝 Connect

**Sushanth Bakka** — [LinkedIn](https://linkedin.com/in/bakkasushanth) · [GitHub](https://github.com/bakkasushanth) · sushanthbakka@gmail.com
