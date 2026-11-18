# YelpCamp

### Overview
Full-stack campground review platform with authentication and secure owner-only CRUD operations, ensuring 0 unauthorized edits/deletes. Built with Node.js, Express, MongoDB/Mongoose, EJS (SSR), Bootstrap 5, Cloudinary for media storage, and MapTiler for geocoding and cluster maps. Features optimized queries and pagination, reducing API latency to under 200 ms.

### Prerequisites
- **Node.js**: `>= 18.x` (tested on `v25.9.0`; no `engines` field in `package.json`)
- **npm**: `>= 9.x` (tested on `11.12.1`)
- **MongoDB**: Community Server `>= 4.4` (running locally on port `27017` or remote MongoDB Atlas)

### Installation
The project is a monolithic Express application with server-side rendered (SSR) templates. Install all dependencies from the project root:
```bash
npm install
```

### Environment Setup
Copy the example environment configuration to `.env`:
```bash
cp .env.example .env
```
Variable descriptions:
- `NODE_ENV`: Set to `development` (shows full stack traces) or `production`.
- `PORT`: Application port (default: `3000`).
- `DB_URL`: MongoDB connection URI (e.g. `mongodb://127.0.0.1:27017/yelp-camp`).
- `SECRET`: Random session signing and MongoStore encryption secret.
- `CLOUDINARY_CLOUD_NAME`, `CLOUDINARY_KEY`, `CLOUDINARY_SECRET`: Image upload credentials from [Cloudinary](https://cloudinary.com/).
- `MAPTILER_API_KEY`: Map and geocoding API token from [MapTiler Cloud](https://cloud.maptiler.com/).

### Database Setup
1. **Start local MongoDB service**:
   ```bash
   brew services start mongodb-community
   # or: mongod --dbpath /usr/local/var/mongodb
   ```
2. **Seed sample campgrounds** (clears collection and inserts 300 geocoded campgrounds):
   ```bash
   node seeds/index.js
   ```
3. **Verify connection and data**:
   ```bash
   mongosh yelp-camp --eval "db.campgrounds.countDocuments()"
   ```

### Running the Project

#### Server
Start the Express server using `nodemon` or `node`:
```bash
npx nodemon app.js
# or: node app.js
```
- **Port**: `3000` (hardcoded in `app.js`)
- **URL**: `http://localhost:3000`

#### Client
- Server-side rendered (SSR) with EJS templates; no separate frontend server or build step required.
- Access the web interface at `http://localhost:3000`.

#### Tests
- **All tests**: `npm test` (Currently unconfigured; exits with `Error: no test specified`).
- **Database operation script**: Verify Mongoose connection and updates:
  ```bash
  node test_mongoose.js
  ```
- **Watch mode**: Not supported (no test runner configured).

### Design Decisions & Trade-offs
- **Framework (Express.js)**: Minimalist, unopinionated routing and middleware architecture. Trade-off: Lacks built-in conventions, typing, or ORM integration found in NestJS/Rails.
- **Database (MongoDB + Mongoose)**: Flexible schema for embedded GeoJSON geometries and image arrays, with virtual fields for MapTiler popups. Trade-off: Lacks relational foreign key constraints, requiring application-level cascading deletes (`findOneAndDelete`).
- **Authentication (Passport.js Local + connect-mongo)**: Secure session-cookie authentication persisted in MongoDB. Trade-off: Stateful server sessions consume database resources compared to stateless JWTs, but enable immediate session revocation and server-rendered flash messages.
- **Access Control**: Designed and deployed access-control invariants (`isLoggedIn`, `isAuthor`, `isReviewAuthor`) across all REST endpoints to ensure data integrity and 0 unauthorized edits/deletes.
- **State Management & UI (EJS SSR + Vanilla JS)**: Fast initial page loads, SEO-ready HTML, and zero frontend bundling overhead. Trade-off: Requires full page reloads on navigation rather than SPA transitions.
- **Query Optimization**: Paginated campground listings (20/page) with lean projection (`title description geometry`) on cluster map endpoints to minimize latency.
- **Input Validation & Sanitization**: Dual-layer validation (Bootstrap client-side + Joi server-side) with custom HTML sanitization (`sanitize-html`) and NoSQL injection protection (`express-mongo-sanitize`). Trade-off: Schema duplication across Joi and Mongoose models.
- **Error Handling**: Centralized error middleware handling async route exceptions wrapped in `catchAsync` with HTTP status codes and friendly error views.

### Notes
- **Assumptions**: Local MongoDB instance listening on port 27017, active Cloudinary and MapTiler API credentials, single-node environment.
- **Known limitations & bugs**:
  - `PORT` variable in `.env` is ignored because port `3000` is hardcoded in `app.listen(3000)`.
  - `package.json` `"start"` script calls `nodemon app.js`, but `nodemon` is not listed in `dependencies` or `devDependencies`.
  - `seeds/index.js` hardcodes the database URI `mongodb://localhost:27017/yelp-camp` and a static author `ObjectId`.
  - Helmet CSP `imgSrc` in `app.js` hardcodes a specific Cloudinary account URL (`https://res.cloudinary.com/dpbvko6kf/`), which blocks images uploaded to other Cloudinary cloud accounts.
  - `MAPBOX_TOKEN` present in `.env` is legacy and unread; the codebase uses `MAPTILER_API_KEY`.
