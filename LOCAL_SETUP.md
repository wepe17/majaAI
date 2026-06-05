# 💻 MAJA.AI — Local Development Setup

**Panduan Lengkap Menjalankan MAJA.AI di Komputer Lokal**

---

## 📋 Daftar Isi

1. [Persiapan Sistem](#persiapan-sistem)
2. [Clone Repository](#clone-repository)
3. [Setup Development (Simple)](#setup-development-simple)
4. [Setup Development (Full Stack)](#setup-development-full-stack)
5. [Troubleshooting](#troubleshooting)

---

## 1. Persiapan Sistem

### ✅ System Requirements

**Minimum:**
- OS: Windows 10/11, macOS 10.15+, Ubuntu 20.04+
- RAM: 8 GB (16 GB recommended)
- Storage: 10 GB free space
- Internet connection untuk download dependencies

**Software yang Dibutuhkan:**

| Software | Versi | Download Link |
|----------|-------|---------------|
| **Git** | 2.30+ | https://git-scm.com/downloads |
| **Web Browser** | Latest | Chrome/Firefox/Edge |

---

## 2. Clone Repository

### 📥 Download Code dari GitHub

#### **Option 1: Via Git Clone (Recommended)**

```bash
# 1. Buka Terminal/Command Prompt/Git Bash
# 2. Navigate ke folder kerja Anda
cd ~/Documents  # macOS/Linux
cd C:\Users\YourName\Documents  # Windows

# 3. Clone repository
git clone https://github.com/yourorg/maja-ai.git

# 4. Masuk ke folder project
cd maja-ai

# 5. Lihat isi folder
ls  # macOS/Linux
dir  # Windows
```

#### **Option 2: Download ZIP**

```bash
# 1. Buka browser, kunjungi:
https://github.com/yourorg/maja-ai

# 2. Klik tombol hijau "Code" → "Download ZIP"
# 3. Extract file ZIP
# 4. Buka folder hasil extract di Terminal/Command Prompt
```

---

## 3. Setup Development (Simple)

### 🚀 Quick Start — Frontend Only (No Backend)

**Cocok untuk:**
- Testing UI/UX
- Design review
- Demo presentation
- Tidak perlu AI backend

#### **Step-by-Step:**

```bash
# 1. Masuk ke folder project
cd maja-ai

# 2. Buka file index.html di browser

# === Windows ===
start index.html

# === macOS ===
open index.html

# === Linux ===
xdg-open index.html

# ATAU: Drag & drop file index.html ke browser window
```

**✅ Done! Browser akan membuka MAJA.AI**

#### **Fitur yang Tersedia (Mode Demo):**

✅ Upload file (UI only, tidak diproses)  
✅ Pilih jenis analisis  
✅ Tulis pertanyaan  
✅ Lihat demo response (pre-generated)  
✅ Charts & visualizations  

❌ File tidak benar-benar di-parse  
❌ AI tidak benar-benar menganalisis  
❌ Response adalah dummy data  

---

### 🌐 Quick Start — Frontend dengan Local Server

**Mengapa perlu local server?**
- Fix CORS issues
- Testing file upload lebih realistis
- Better development experience

#### **Method 1: Python (Recommended — Paling Mudah)**

```bash
# 1. Check apakah Python sudah terinstall
python --version
# atau
python3 --version

# Jika belum ada, download dari: https://www.python.org/downloads/

# 2. Jalankan HTTP server di folder project
cd maja-ai
python -m http.server 8000
# atau jika python3:
python3 -m http.server 8000

# 3. Buka browser, kunjungi:
http://localhost:8000
```

**Output yang diharapkan:**
```
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

**Stop server:** Tekan `Ctrl + C` di terminal

---

#### **Method 2: Node.js (http-server)**

```bash
# 1. Check apakah Node.js sudah terinstall
node --version

# Jika belum ada, download dari: https://nodejs.org/

# 2. Install http-server (sekali saja)
npm install -g http-server

# 3. Jalankan server
cd maja-ai
http-server -p 8000

# 4. Buka browser:
http://localhost:8000
```

---

#### **Method 3: PHP (jika sudah terinstall)**

```bash
# 1. Check PHP
php --version

# 2. Jalankan server
cd maja-ai
php -S localhost:8000

# 3. Buka browser:
http://localhost:8000
```

---

#### **Method 4: VS Code Live Server Extension**

```bash
# 1. Install VS Code: https://code.visualstudio.com/

# 2. Install Extension "Live Server" by Ritwick Dey
# Cara: Extensions panel (Ctrl+Shift+X) → Search "Live Server" → Install

# 3. Buka folder maja-ai di VS Code
code maja-ai

# 4. Klik kanan file index.html → "Open with Live Server"

# 5. Browser otomatis terbuka di:
http://127.0.0.1:5500
```

**Keuntungan Live Server:**
- Auto-reload saat file berubah
- Tidak perlu refresh manual
- Cocok untuk development

---

## 4. Setup Development (Full Stack)

### 🔧 Full Stack Setup — Frontend + Backend + AI

**Cocok untuk:**
- Development aktif
- Testing real AI integration
- Full features testing
- Production-like environment

---

### **Prerequisites:**

| Software | Versi | Fungsi |
|----------|-------|--------|
| **Python** | 3.11+ | Backend API |
| **Node.js** | 20 LTS | Frontend development |
| **Docker** | 24+ | Services (optional) |
| **PostgreSQL** | 15+ | Database (optional) |
| **Git** | 2.30+ | Version control |

---

### **Step 1: Install Required Software**

#### **Python 3.11+**

```bash
# === Windows ===
# Download dari: https://www.python.org/downloads/
# Jangan lupa centang "Add Python to PATH"

# Verify:
python --version
# Output: Python 3.11.x

# === macOS (via Homebrew) ===
brew install python@3.11

# === Ubuntu/Debian ===
sudo apt update
sudo apt install python3.11 python3.11-venv python3-pip
```

#### **Node.js 20 LTS**

```bash
# === Windows & macOS ===
# Download dari: https://nodejs.org/

# Verify:
node --version  # v20.x.x
npm --version   # 10.x.x

# === Ubuntu/Debian ===
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
```

#### **Docker (Optional, tapi Recommended)**

```bash
# === Windows & macOS ===
# Download Docker Desktop: https://www.docker.com/products/docker-desktop/

# === Ubuntu/Debian ===
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Verify:
docker --version
docker-compose --version
```

---

### **Step 2: Clone dan Setup Project**

```bash
# 1. Clone repository
git clone https://github.com/yourorg/maja-ai.git
cd maja-ai

# 2. Lihat struktur folder
tree -L 2  # atau: ls -la

# Expected structure:
# maja-ai/
# ├── frontend/          # Next.js application
# ├── backend/           # FastAPI application
# ├── docker-compose.yml # Docker services
# ├── index.html         # Standalone demo
# └── README.md
```

---

### **Step 3: Setup Backend (Python FastAPI)**

```bash
# 1. Masuk ke folder backend
cd backend

# 2. Buat virtual environment
python -m venv venv
# atau python3:
python3 -m venv venv

# 3. Aktifkan virtual environment
# === Windows (Command Prompt) ===
venv\Scripts\activate.bat

# === Windows (PowerShell) ===
venv\Scripts\Activate.ps1

# === macOS / Linux ===
source venv/bin/activate

# Setelah aktif, prompt akan berubah jadi: (venv) ...

# 4. Upgrade pip
pip install --upgrade pip

# 5. Install dependencies
pip install -r requirements.txt

# Tunggu proses install (5-10 menit, tergantung koneksi)
```

#### **Configure Environment Variables**

```bash
# 6. Copy .env.example ke .env
cp .env.example .env  # macOS/Linux
copy .env.example .env  # Windows

# 7. Edit .env file
nano .env  # atau gunakan text editor favorit

# Minimal configuration:
OPENAI_API_KEY=sk-your-api-key-here
DATABASE_URL=sqlite:///./maja.db  # Gunakan SQLite untuk development
UPLOAD_DIR=./storage/uploads
VECTORDB_DIR=./storage/vectordb
```

**Cara Mendapatkan OpenAI API Key:**

1. Kunjungi: https://platform.openai.com/
2. Sign up / Login
3. Klik "API Keys" di menu
4. Klik "Create new secret key"
5. Copy key dan paste ke `.env`

#### **Run Backend Server**

```bash
# 8. Jalankan database migrations (jika ada)
alembic upgrade head

# 9. Start backend server
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000

# Expected output:
# INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
# INFO:     Started reloader process
# INFO:     Started server process
# INFO:     Waiting for application startup.
# INFO:     Application startup complete.
```

**Test Backend:**

```bash
# Buka browser atau gunakan curl:
curl http://localhost:8000/health

# Expected response:
{"status":"ok","message":"MAJA.AI Backend is running"}
```

**Keep terminal ini tetap buka!** Backend harus running.

---

### **Step 4: Setup Frontend (Next.js)**

**Buka terminal BARU** (backend tetap running di terminal pertama)

```bash
# 1. Masuk ke folder frontend
cd maja-ai/frontend

# 2. Install dependencies
npm install
# atau gunakan yarn:
yarn install

# Tunggu proses install (5-10 menit)

# 3. Copy environment variables
cp .env.example .env.local

# 4. Edit .env.local
nano .env.local

# Set API URL:
NEXT_PUBLIC_API_URL=http://localhost:8000
```

#### **Run Frontend Development Server**

```bash
# 5. Start frontend server
npm run dev
# atau:
yarn dev

# Expected output:
#   ▲ Next.js 14.2.5
#   - Local:        http://localhost:3000
#   - Ready in 2.3s
```

**Test Frontend:**

```bash
# Buka browser:
http://localhost:3000
```

**✅ Done! Full stack MAJA.AI running locally!**

---

### **Step 5: Setup Services dengan Docker (Recommended)**

**Mengapa Docker?**
- Setup PostgreSQL, Redis, ChromaDB dengan 1 command
- Consistent environment
- Easy to reset/restart

#### **Docker Compose Setup**

```bash
# 1. Pastikan Docker Desktop running

# 2. Kembali ke root folder project
cd maja-ai

# 3. Start all services
docker-compose up -d

# Services yang akan dijalankan:
# - PostgreSQL (port 5432)
# - Redis (port 6379)
# - ChromaDB (port 8001)
# - MinIO (port 9000, 9001)

# 4. Check status
docker-compose ps

# Expected output:
# NAME                 STATUS              PORTS
# maja-ai-postgres-1   Up 10 seconds       0.0.0.0:5432->5432/tcp
# maja-ai-redis-1      Up 10 seconds       0.0.0.0:6379->6379/tcp
# maja-ai-chromadb-1   Up 10 seconds       0.0.0.0:8001->8000/tcp
# maja-ai-minio-1      Up 10 seconds       0.0.0.0:9000-9001->9000-9001/tcp

# 5. View logs (optional)
docker-compose logs -f

# Stop services (ketika selesai):
docker-compose down
```

#### **Update Backend .env untuk Docker Services**

```bash
# Edit backend/.env
DATABASE_URL=postgresql://majaai:password@localhost:5432/majaai
REDIS_URL=redis://localhost:6379
CHROMADB_URL=http://localhost:8001
MINIO_ENDPOINT=localhost:9000
```

---

## 5. Troubleshooting

### ❌ Common Errors & Solutions

#### **Error: "Python not found"**

```bash
# Windows: Install dari https://www.python.org/
# Pastikan centang "Add Python to PATH"

# macOS:
brew install python@3.11

# Linux:
sudo apt install python3.11
```

---

#### **Error: "pip: command not found"**

```bash
# Gunakan python -m pip sebagai gantinya:
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

---

#### **Error: "venv/Scripts/activate.ps1 cannot be loaded"**

PowerShell execution policy issue (Windows):

```powershell
# Run PowerShell as Administrator, jalankan:
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser

# Lalu coba lagi:
venv\Scripts\Activate.ps1
```

---

#### **Error: "Port 8000 already in use"**

```bash
# Cari process yang menggunakan port 8000:

# Windows:
netstat -ano | findstr :8000
taskkill /PID <PID> /F

# macOS/Linux:
lsof -i :8000
kill -9 <PID>

# Atau gunakan port lain:
uvicorn app.main:app --port 8001
```

---

#### **Error: "OPENAI_API_KEY not found"**

```bash
# Pastikan .env file sudah dibuat dan berisi:
OPENAI_API_KEY=sk-your-actual-key-here

# Jangan gunakan quotes:
# ✅ OPENAI_API_KEY=sk-abc123
# ❌ OPENAI_API_KEY="sk-abc123"
```

---

#### **Error: "npm: command not found"**

```bash
# Install Node.js dari: https://nodejs.org/
# Restart terminal setelah install
node --version
npm --version
```

---

#### **Error: "docker-compose: command not found"**

```bash
# Install Docker Desktop: https://www.docker.com/products/docker-desktop/
# Atau coba:
docker compose up -d  # (tanpa hyphen, Docker Compose v2)
```

---

#### **Error: "Cannot connect to database"**

```bash
# Check apakah PostgreSQL running:
docker-compose ps

# Jika tidak running, start ulang:
docker-compose up -d postgres

# Check connection:
docker-compose exec postgres psql -U majaai -d majaai
```

---

#### **Error: "Module not found" atau "Import error"**

```bash
# Pastikan virtual environment aktif:
which python  # harus menunjuk ke venv/bin/python

# Reinstall dependencies:
pip install -r requirements.txt

# Clear cache dan reinstall:
pip cache purge
pip install --no-cache-dir -r requirements.txt
```

---

### 🔍 Verification Checklist

```bash
# ✅ Checklist untuk memastikan semua berjalan:

# 1. Backend running
curl http://localhost:8000/health
# Expected: {"status":"ok"}

# 2. Frontend running
curl http://localhost:3000
# Expected: HTML content

# 3. PostgreSQL accessible
docker-compose exec postgres psql -U majaai -d majaai -c "SELECT 1;"
# Expected: 1

# 4. Redis accessible
docker-compose exec redis redis-cli ping
# Expected: PONG

# 5. ChromaDB accessible
curl http://localhost:8001/api/v1/heartbeat
# Expected: {"nanosecond heartbeat": ...}

# 6. MinIO accessible
curl http://localhost:9000/minio/health/live
# Expected: Empty response (200 OK)
```

---

## 📂 Project Structure

```
maja-ai/
├── frontend/                   # Next.js frontend
│   ├── src/
│   │   ├── app/               # Next.js app directory
│   │   ├── components/        # React components
│   │   ├── lib/               # Utilities & API client
│   │   └── store/             # State management
│   ├── package.json
│   └── .env.local
│
├── backend/                    # FastAPI backend
│   ├── app/
│   │   ├── main.py            # FastAPI app entry
│   │   ├── config.py          # Configuration
│   │   ├── models/            # Database models
│   │   ├── routers/           # API routes
│   │   ├── services/          # Business logic
│   │   └── utils/             # Utilities
│   ├── requirements.txt
│   ├── .env
│   └── venv/                  # Virtual environment
│
├── index.html                  # Standalone demo (frontend only)
├── docker-compose.yml          # Docker services
├── README.md
├── LOCAL_SETUP.md             # This file
└── INFRASTRUCTURE.md
```

---

## 🎯 Development Workflow

### **Daily Development Routine:**

```bash
# ═══════════════════════════════════════════════════════════
# MORNING — Start Development
# ═══════════════════════════════════════════════════════════

# 1. Pull latest code
git pull origin main

# 2. Start Docker services (Terminal 1)
docker-compose up -d

# 3. Start backend (Terminal 2)
cd backend
source venv/bin/activate  # atau venv\Scripts\activate di Windows
uvicorn app.main:app --reload --port 8000

# 4. Start frontend (Terminal 3)
cd frontend
npm run dev

# 5. Open browser
open http://localhost:3000

# ═══════════════════════════════════════════════════════════
# DURING DEVELOPMENT
# ═══════════════════════════════════════════════════════════

# Backend changes → auto-reload (thanks to --reload)
# Frontend changes → auto-reload (thanks to Next.js)

# View logs:
# - Terminal 2: Backend logs
# - Terminal 3: Frontend logs
docker-compose logs -f  # Docker services logs

# ═══════════════════════════════════════════════════════════
# EVENING — Stop Development
# ═══════════════════════════════════════════════════════════

# 1. Commit changes
git add .
git commit -m "feat: implemented X feature"
git push origin main

# 2. Stop servers
# Terminal 2: Ctrl+C (stop backend)
# Terminal 3: Ctrl+C (stop frontend)

# 3. Stop Docker services
docker-compose down
```

---

## 🚀 Quick Commands Reference

```bash
# ─── Git Commands ───────────────────────────────────────────
git clone <repo-url>           # Clone repository
git pull origin main           # Update code
git status                     # Check changes
git add .                      # Stage all changes
git commit -m "message"        # Commit changes
git push origin main           # Push to GitHub

# ─── Python/Backend ─────────────────────────────────────────
python -m venv venv            # Create virtual env
source venv/bin/activate       # Activate (Mac/Linux)
venv\Scripts\activate          # Activate (Windows)
pip install -r requirements.txt # Install dependencies
uvicorn app.main:app --reload  # Start backend
deactivate                     # Deactivate venv

# ─── Node.js/Frontend ───────────────────────────────────────
npm install                    # Install dependencies
npm run dev                    # Start dev server
npm run build                  # Build for production
npm run start                  # Start production server

# ─── Docker ─────────────────────────────────────────────────
docker-compose up -d           # Start services (background)
docker-compose down            # Stop services
docker-compose ps              # Check status
docker-compose logs -f         # View logs
docker-compose restart         # Restart services

# ─── Useful ─────────────────────────────────────────────────
python -m http.server 8000     # Simple HTTP server
curl http://localhost:8000/health  # Test backend
lsof -i :8000                  # Check port usage (Mac/Linux)
netstat -ano | findstr :8000   # Check port usage (Windows)
```

---

## 📞 Need Help?

### **Resources:**

- 📚 **Full Docs:** [INFRASTRUCTURE.md](./INFRASTRUCTURE.md)
- 🚀 **Quick Start:** [README.md](./README.md)
- 💡 **Summary:** [INFRASTRUCTURE_SUMMARY.md](./INFRASTRUCTURE_SUMMARY.md)

### **Common Issues:**

1. **Backend tidak connect ke database** → Check `docker-compose ps`
2. **Frontend tidak bisa call API** → Check CORS settings di backend
3. **OpenAI API error** → Check API key di `.env`
4. **Port conflict** → Gunakan port lain atau kill process

### **Best Practices:**

✅ Gunakan virtual environment untuk Python  
✅ Commit code secara berkala  
✅ Stop Docker services saat tidak digunakan (hemat resource)  
✅ Backup `.env` file (jangan commit ke Git!)  
✅ Update dependencies secara berkala  

---

<div align="center">

## 🏛️ MAJA.AI — Local Development Ready!

**Simple Setup** | **Full Stack** | **Docker Support**

**Clone → Install → Run** 🚀

---

*Happy Coding! Selamat mengembangkan MAJA.AI! 💻✨*

</div>
