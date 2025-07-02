# 🚀 Vercel-Like Monorepo

A monorepo for a Vercel-inspired deployment platform. Clone, upload, deploy, and run static sites from any public git repository, with a modern web UI and scalable backend.

---

## 🏗️ Architecture

- **📤 uploadService**:  
  - Accepts a git repository URL, clones it, and uploads the contents to a Cloudflare R2 bucket ☁️.
  - Uses Redis for build queueing and status tracking 🗃️.
- **⚙️ deployment-service**:  
  - Listens to the Redis build queue, downloads files from R2, builds the project, and uploads the final static site to R2 🚀.
- **🌐 request-handler-service**:  
  - Serves deployed static sites from R2, acting as a CDN edge (can be fronted by CloudFront or similar) 🌍.
- **🖥️ frontend**:  
  - React + Vite + Tailwind CSS UI for users to submit git repos, track deployment, and get live URLs 💻.

---

## ✨ Features

- ☁️ **Cloudflare R2** for all file storage (upload, build, serve)
- 🗃️ **Redis** queue for scalable, decoupled build/deploy pipeline
- 🐙 **Git integration**: clone any public repo, auto-deploy
- 🌍 **CDN-ready**: request handler can be fronted by CloudFront or similar
- 🖥️ **Modern UI**: Deploy and manage sites like Vercel

---

## 📁 Directory Structure

```
vercel/
  deployment-service/      # Build and deploy logic, Redis queue, R2 integration
  request-handler-service/ # Serves static sites from R2, CDN edge
  uploadService/           # Git clone, upload to R2, queue jobs
  frontend/                # React + Vite + Tailwind web UI
```

---

## 🚦 Getting Started

### 🛠️ Prerequisites

- Node.js (v16+)
- npm or yarn
- Redis server 🗃️
- Cloudflare R2 credentials ☁️ (or compatible S3 API)

### 📦 Installation

Clone the repository:
```bash
git clone <your-repo-url>
cd vercel
```

Install dependencies for each package:
```bash
cd deployment-service && npm install
cd ../request-handler-service && npm install
cd ../uploadService && npm install
cd ../frontend && npm install
```

### 🔑 Environment Variables

Create a `.env` file in each backend service with:
```
AWS_ACCESS_KEY_ID=<your-r2-access-key>
AWS_SECRET_ACCESS_KEY=<your-r2-secret-key>
S3_ENDPOINT=https://<your-account-id>.r2.cloudflarestorage.com
S3_BUCKET=<your-bucket-name>
REDIS_URL=redis://localhost:6379
```

---

## ▶️ Running Services

Open separate terminals for each service:

**📤 Upload Service:**
```bash
cd uploadService
npm start
```

**⚙️ Deployment Service:**
```bash
cd deployment-service
npm start
```

**🌐 Request Handler Service:**
```bash
cd request-handler-service
npm start
```

**🖥️ Frontend:**
```bash
cd frontend
npm run dev
```

---

## 🧑‍💻 Usage

1. Open the frontend at [http://localhost:5173](http://localhost:5173) 🖥️.
2. Enter a public git repository URL 🐙 and click "Upload/Deploy".
3. The backend will:
   - Clone the repo
   - Upload files to Cloudflare R2 ☁️
   - Queue a build job in Redis 🗃️
   - Build and deploy the site 🚀
   - Serve the site from R2 via the request handler (CDN-ready) 🌍
4. Get a live URL for your deployed site.

---

## 🛠️ Technologies Used

- **Backend:** Node.js, TypeScript, Express, Redis 🗃️, Cloudflare R2 ☁️ (S3 API), simple-git 🐙
- **Frontend:** React, Vite, Tailwind CSS 🖥️
- **Queue:** Redis 🗃️
- **Storage:** Cloudflare R2 ☁️
- **CDN:** CloudFront 🌍 (optional, for production)

---

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/YourFeature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/YourFeature`)
5. Open a Pull Request

---

## 📄 License

[MIT](LICENSE)
