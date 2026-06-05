# 🏗️ MAJA.AI — Infrastruktur Sistem

**Dokumentasi Lengkap Kebutuhan Infrastruktur & Arsitektur Sistem**

---

## 📋 Daftar Isi

1. [Arsitektur Sistem](#arsitektur-sistem)
2. [Technology Stack](#technology-stack)
3. [Infrastruktur Hardware](#infrastruktur-hardware)
4. [Infrastruktur Software](#infrastruktur-software)
5. [Database & Storage](#database--storage)
6. [Networking & Security](#networking--security)
7. [Deployment Scenarios](#deployment-scenarios)
8. [Scalability & Performance](#scalability--performance)
9. [Monitoring & Logging](#monitoring--logging)
10. [Backup & Disaster Recovery](#backup--disaster-recovery)
11. [Cost Estimation](#cost-estimation)

---

## 1. Arsitektur Sistem

### 🏛️ Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                         USER LAYER                              │
│  Web Browser (Chrome, Firefox, Safari, Edge)                    │
└────────────┬────────────────────────────────────────────────────┘
             │ HTTPS
             ↓
┌─────────────────────────────────────────────────────────────────┐
│                      PRESENTATION LAYER                         │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  Frontend Web Application (Next.js / React)              │  │
│  │  - Single Page Application (SPA)                         │  │
│  │  - Responsive UI dengan Material Design                  │  │
│  │  - Real-time updates via WebSocket                       │  │
│  └──────────────────────────────────────────────────────────┘  │
└────────────┬────────────────────────────────────────────────────┘
             │ REST API / GraphQL
             ↓
┌─────────────────────────────────────────────────────────────────┐
│                      APPLICATION LAYER                          │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  API Gateway (Nginx / Kong / AWS API Gateway)           │  │
│  │  - Load Balancing                                        │  │
│  │  - Rate Limiting                                         │  │
│  │  - SSL/TLS Termination                                   │  │
│  │  - Request Routing                                       │  │
│  └──────────────────────────────────────────────────────────┘  │
│                                                                 │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  Backend API Server (Python FastAPI)                    │  │
│  │  - RESTful API Endpoints                                │  │
│  │  - Business Logic                                        │  │
│  │  - Authentication & Authorization                        │  │
│  │  - Session Management                                    │  │
│  └──────────────────────────────────────────────────────────┘  │
└────────────┬────────────────────────────────────────────────────┘
             │
             ↓
┌─────────────────────────────────────────────────────────────────┐
│                       SERVICE LAYER                             │
│  ┌─────────────────┐  ┌─────────────────┐  ┌────────────────┐  │
│  │ Document        │  │ RAG Service     │  │ AI Service     │  │
│  │ Processor       │  │ (LangChain)     │  │ (OpenAI)       │  │
│  │ - PDF Parser    │  │ - Embeddings    │  │ - GPT-4o       │  │
│  │ - Excel Parser  │  │ - Vector Search │  │ - Completion   │  │
│  │ - CSV Parser    │  │ - Context Build │  │ - Streaming    │  │
│  │ - Text Extract  │  │ - Retrieval     │  │ - Token Mgmt   │  │
│  └─────────────────┘  └─────────────────┘  └────────────────┘  │
└────────────┬────────────────────────────────────────────────────┘
             │
             ↓
┌─────────────────────────────────────────────────────────────────┐
│                        DATA LAYER                               │
│  ┌─────────────────┐  ┌─────────────────┐  ┌────────────────┐  │
│  │ PostgreSQL      │  │ ChromaDB        │  │ Redis Cache    │  │
│  │ - User Data     │  │ - Embeddings    │  │ - Sessions     │  │
│  │ - Metadata      │  │ - Vector Store  │  │ - Rate Limit   │  │
│  │ - Audit Logs    │  │ - Document DB   │  │ - Temp Data    │  │
│  └─────────────────┘  └─────────────────┘  └────────────────┘  │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ Object Storage (MinIO / S3 / Azure Blob)               │   │
│  │ - Uploaded Documents (PDF, Excel, CSV)                 │   │
│  │ - Generated Reports                                     │   │
│  │ - User Attachments                                      │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

---

## 2. Technology Stack

### 🎯 Frontend Stack

| Komponen | Teknologi | Versi | Fungsi |
|----------|-----------|-------|--------|
| **Framework** | Next.js | 14.x | Server-side rendering, routing |
| **UI Library** | React | 18.x | Component-based UI |
| **State Management** | Zustand / Redux Toolkit | Latest | Global state management |
| **Styling** | Tailwind CSS | 3.x | Utility-first CSS framework |
| **HTTP Client** | Axios | 1.x | API requests |
| **Charts** | Chart.js | 4.x | Data visualization |
| **Icons** | Material Icons | Latest | Icon library |
| **Forms** | React Hook Form | 7.x | Form validation |
| **File Upload** | React Dropzone | 14.x | Drag & drop uploads |
| **Markdown** | React Markdown | 9.x | Render markdown content |

### ⚙️ Backend Stack

| Komponen | Teknologi | Versi | Fungsi |
|----------|-----------|-------|--------|
| **Framework** | FastAPI | 0.111.x | High-performance API framework |
| **Language** | Python | 3.11+ | Backend programming language |
| **ASGI Server** | Uvicorn | 0.30.x | Production ASGI server |
| **ORM** | SQLAlchemy | 2.x | Database ORM |
| **Migration** | Alembic | 1.x | Database migrations |
| **Auth** | Python-Jose + Passlib | Latest | JWT + password hashing |
| **Validation** | Pydantic | 2.x | Data validation |
| **Task Queue** | Celery | 5.x | Async task processing |
| **Message Broker** | RabbitMQ / Redis | Latest | Task queue backend |

### 🤖 AI & ML Stack

| Komponen | Teknologi | Versi | Fungsi |
|----------|-----------|-------|--------|
| **LLM Provider** | OpenAI API | Latest | GPT-4o, GPT-4-turbo |
| **RAG Framework** | LangChain | 0.2.x | RAG orchestration |
| **Embeddings** | OpenAI Embeddings | text-embedding-3-small | Vector embeddings |
| **Vector Database** | ChromaDB | 0.5.x | Vector similarity search |
| **Document Parsers** | PyPDF, openpyxl, pandas | Latest | File parsing |
| **Text Processing** | NLTK / spaCy | Latest | NLP preprocessing (optional) |

### 💾 Database & Storage

| Komponen | Teknologi | Versi | Fungsi |
|----------|-----------|-------|--------|
| **Primary Database** | PostgreSQL | 15.x / 16.x | Relational data |
| **Vector Store** | ChromaDB | 0.5.x | Embeddings & vectors |
| **Cache** | Redis | 7.x | Session & caching |
| **Object Storage** | MinIO / S3 | Latest | File storage |
| **Backup** | pg_dump / rsync | Native | Database backup |

### 🌐 Infrastructure & DevOps

| Komponen | Teknologi | Fungsi |
|----------|-----------|--------|
| **Container** | Docker | Containerization |
| **Orchestration** | Docker Compose / Kubernetes | Container orchestration |
| **Reverse Proxy** | Nginx / Caddy | Load balancing, SSL |
| **CI/CD** | GitHub Actions / GitLab CI | Automated deployment |
| **Monitoring** | Prometheus + Grafana | Metrics & dashboards |
| **Logging** | ELK Stack (Elasticsearch, Logstash, Kibana) | Centralized logging |
| **APM** | Sentry | Error tracking |

---

## 3. Infrastruktur Hardware

### 🖥️ Server Requirements

#### **Scenario 1: Development/Testing (Single Server)**

```
Purpose: Development, testing, small-scale demo
Users: < 10 concurrent users
```

| Komponen | Spesifikasi | Rekomendasi |
|----------|-------------|-------------|
| **CPU** | 4 vCPU / Cores | Intel Xeon / AMD EPYC |
| **RAM** | 16 GB | DDR4 2666MHz+ |
| **Storage** | 500 GB SSD | NVMe SSD preferred |
| **Network** | 1 Gbps | Dedicated bandwidth |
| **OS** | Ubuntu 22.04 LTS / Rocky Linux 9 | 64-bit |

**Estimasi Biaya:** Rp 500K - 1.5 juta/bulan (VPS Cloud)

---

#### **Scenario 2: Production Small (10-50 Users)**

```
Purpose: Single pemda (kabupaten/kota kecil)
Users: 10-50 concurrent users
Documents: < 10,000 files
```

**Architecture:** 2 Server Setup

**Server 1: Application Server**
| Komponen | Spesifikasi |
|----------|-------------|
| CPU | 8 vCPU |
| RAM | 32 GB |
| Storage | 500 GB SSD |
| Role | Frontend + Backend + Redis |

**Server 2: Database & Storage**
| Komponen | Spesifikasi |
|----------|-------------|
| CPU | 4 vCPU |
| RAM | 16 GB |
| Storage | 1 TB SSD (RAID 1) |
| Role | PostgreSQL + ChromaDB + MinIO |

**Estimasi Biaya:** Rp 2-4 juta/bulan (2 VPS)

---

#### **Scenario 3: Production Medium (50-200 Users)**

```
Purpose: Multiple pemda / provinsi
Users: 50-200 concurrent users
Documents: 10,000 - 100,000 files
```

**Architecture:** 4 Server Setup + Load Balancer

**Load Balancer**
| Komponen | Spesifikasi |
|----------|-------------|
| CPU | 2 vCPU |
| RAM | 4 GB |
| Role | Nginx reverse proxy |

**App Servers (2x)**
| Komponen | Spesifikasi |
|----------|-------------|
| CPU | 8 vCPU each |
| RAM | 32 GB each |
| Storage | 200 GB SSD each |
| Role | Frontend + Backend (load balanced) |

**Database Server**
| Komponen | Spesifikasi |
|----------|-------------|
| CPU | 8 vCPU |
| RAM | 64 GB |
| Storage | 2 TB SSD (RAID 10) |
| Role | PostgreSQL (primary) |

**Storage & Vector DB Server**
| Komponen | Spesifikasi |
|----------|-------------|
| CPU | 8 vCPU |
| RAM | 32 GB |
| Storage | 4 TB SSD |
| Role | ChromaDB + MinIO + Redis |

**Estimasi Biaya:** Rp 10-20 juta/bulan

---

#### **Scenario 4: Production Large (200-1000+ Users)**

```
Purpose: National deployment / multiple provinces
Users: 200-1000+ concurrent users
Documents: 100,000+ files
```

**Architecture:** Kubernetes Cluster (Microservices)

**Control Plane** (3 nodes for HA)
| Komponen | Spesifikasi per Node |
|----------|---------------------|
| CPU | 4 vCPU |
| RAM | 16 GB |
| Storage | 200 GB SSD |

**Worker Nodes** (6+ nodes)
| Komponen | Spesifikasi per Node |
|----------|---------------------|
| CPU | 16 vCPU |
| RAM | 64 GB |
| Storage | 500 GB NVMe SSD |

**Database Cluster** (PostgreSQL HA)
- 3 nodes (1 primary, 2 replicas)
- 16 vCPU, 128 GB RAM, 4 TB SSD each

**Object Storage Cluster** (MinIO HA)
- 4 nodes
- 8 vCPU, 32 GB RAM, 8 TB HDD each

**Estimasi Biaya:** Rp 50-100 juta/bulan

---

### 💿 Storage Requirements

#### **Per Document Storage Estimate**

```
Average Document Sizes:
- PDF: 2-5 MB
- Excel: 0.5-2 MB
- CSV: 0.1-1 MB

Embeddings/Vectors:
- Per chunk (1000 chars): ~6 KB (1536 dimensions float32)
- Average document: 10 chunks = 60 KB
```

#### **Storage Calculation by Scale**

| Scale | Documents | Raw Files | Embeddings | Total Storage |
|-------|-----------|-----------|------------|---------------|
| **Small** | 1,000 | ~3 GB | ~60 MB | ~5 GB |
| **Medium** | 10,000 | ~30 GB | ~600 MB | ~50 GB |
| **Large** | 100,000 | ~300 GB | ~6 GB | ~500 GB |
| **Enterprise** | 1,000,000+ | ~3 TB | ~60 GB | ~5 TB |

**Rekomendasi:** Provision 3x storage needs untuk growth + backups

---

## 4. Infrastruktur Software

### 🐧 Operating System

**Rekomendasi Primary:**
- **Ubuntu Server 22.04 LTS** (Most supported, easiest)
- **Rocky Linux 9** atau **AlmaLinux 9** (Enterprise, RHEL-compatible)

**Requirements:**
- 64-bit
- Kernel 5.15+
- Systemd
- OpenSSH

---

### 🐳 Containerization

**Docker Setup:**

```yaml
# docker-compose.yml (Production)
version: '3.8'

services:
  # Frontend
  frontend:
    image: maja-ai/frontend:latest
    ports:
      - "3000:3000"
    environment:
      - NEXT_PUBLIC_API_URL=http://backend:8000
    depends_on:
      - backend
    restart: unless-stopped

  # Backend API
  backend:
    image: maja-ai/backend:latest
    ports:
      - "8000:8000"
    environment:
      - DATABASE_URL=postgresql://user:pass@postgres:5432/majaai
      - REDIS_URL=redis://redis:6379
      - OPENAI_API_KEY=${OPENAI_API_KEY}
    volumes:
      - ./storage/uploads:/app/storage/uploads
      - ./storage/vectordb:/app/storage/vectordb
    depends_on:
      - postgres
      - redis
      - chromadb
    restart: unless-stopped

  # PostgreSQL Database
  postgres:
    image: postgres:16
    environment:
      - POSTGRES_USER=majaai
      - POSTGRES_PASSWORD=${DB_PASSWORD}
      - POSTGRES_DB=majaai
    volumes:
      - postgres_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"
    restart: unless-stopped

  # ChromaDB Vector Store
  chromadb:
    image: chromadb/chroma:latest
    volumes:
      - chroma_data:/chroma/chroma
    ports:
      - "8001:8000"
    environment:
      - ALLOW_RESET=TRUE
      - ANONYMIZED_TELEMETRY=FALSE
    restart: unless-stopped

  # Redis Cache
  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data
    restart: unless-stopped

  # MinIO Object Storage
  minio:
    image: minio/minio:latest
    ports:
      - "9000:9000"
      - "9001:9001"
    environment:
      - MINIO_ROOT_USER=${MINIO_ROOT_USER}
      - MINIO_ROOT_PASSWORD=${MINIO_ROOT_PASSWORD}
    volumes:
      - minio_data:/data
    command: server /data --console-address ":9001"
    restart: unless-stopped

  # Nginx Reverse Proxy
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
      - ./ssl:/etc/nginx/ssl:ro
    depends_on:
      - frontend
      - backend
    restart: unless-stopped

volumes:
  postgres_data:
  chroma_data:
  redis_data:
  minio_data:
```

---

### 🔧 System Dependencies

#### **Backend Server (Python)**

```bash
# System packages (Ubuntu/Debian)
apt-get install -y \
    python3.11 \
    python3.11-venv \
    python3-pip \
    build-essential \
    libpq-dev \
    libssl-dev \
    libffi-dev \
    libjpeg-dev \
    zlib1g-dev \
    git \
    curl \
    wget

# Python packages (via pip)
pip install \
    fastapi[all]==0.111.0 \
    uvicorn[standard]==0.30.1 \
    sqlalchemy==2.0.30 \
    psycopg2-binary==2.9.9 \
    redis==5.0.4 \
    langchain==0.2.5 \
    langchain-openai==0.1.9 \
    langchain-community==0.2.5 \
    chromadb==0.5.3 \
    openai==1.35.3 \
    pypdf==4.2.0 \
    openpyxl==3.1.4 \
    pandas==2.2.2 \
    celery==5.4.0 \
    python-multipart==0.0.9 \
    python-jose[cryptography]==3.3.0 \
    passlib[bcrypt]==1.7.4 \
    pydantic==2.7.4 \
    pydantic-settings==2.3.3
```

#### **Frontend Server (Node.js)**

```bash
# Node.js 20 LTS
curl -fsSL https://deb.nodesource.com/setup_20.x | bash -
apt-get install -y nodejs

# Yarn package manager
npm install -g yarn

# PM2 process manager
npm install -g pm2
```

---

## 5. Database & Storage

### 🗄️ PostgreSQL Configuration

**Database Schema:**

```sql
-- Users table
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    username VARCHAR(100) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    full_name VARCHAR(255),
    organization VARCHAR(255),
    role VARCHAR(50) DEFAULT 'user',
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Sessions table
CREATE TABLE sessions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    session_name VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Documents table
CREATE TABLE documents (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    session_id UUID REFERENCES sessions(id) ON DELETE CASCADE,
    filename VARCHAR(500) NOT NULL,
    file_path VARCHAR(1000) NOT NULL,
    file_type VARCHAR(50),
    file_size BIGINT,
    upload_status VARCHAR(50) DEFAULT 'pending',
    chunks_created INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Analysis history
CREATE TABLE analysis_history (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    session_id UUID REFERENCES sessions(id) ON DELETE CASCADE,
    analysis_type VARCHAR(100),
    user_prompt TEXT,
    ai_response TEXT,
    tokens_used INTEGER,
    processing_time_ms INTEGER,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Audit logs
CREATE TABLE audit_logs (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id),
    action VARCHAR(100),
    resource_type VARCHAR(100),
    resource_id UUID,
    ip_address INET,
    user_agent TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Create indexes
CREATE INDEX idx_sessions_user_id ON sessions(user_id);
CREATE INDEX idx_documents_session_id ON documents(session_id);
CREATE INDEX idx_analysis_session_id ON analysis_history(session_id);
CREATE INDEX idx_audit_logs_user_id ON audit_logs(user_id);
CREATE INDEX idx_audit_logs_created_at ON audit_logs(created_at);
```

**PostgreSQL Configuration (postgresql.conf):**

```ini
# Connection Settings
max_connections = 200
shared_buffers = 8GB              # 25% of RAM
effective_cache_size = 24GB       # 75% of RAM
maintenance_work_mem = 2GB
checkpoint_completion_target = 0.9
wal_buffers = 16MB
default_statistics_target = 100
random_page_cost = 1.1            # For SSD
effective_io_concurrency = 200
work_mem = 41943kB
min_wal_size = 1GB
max_wal_size = 4GB

# Logging
logging_collector = on
log_directory = 'log'
log_filename = 'postgresql-%Y-%m-%d_%H%M%S.log'
log_rotation_age = 1d
log_rotation_size = 100MB
log_line_prefix = '%t [%p]: [%l-1] user=%u,db=%d,app=%a,client=%h '
log_checkpoints = on
log_connections = on
log_disconnections = on
log_duration = off
log_lock_waits = on
```

---

### 📦 Object Storage (MinIO)

**MinIO Configuration:**

```bash
# Create buckets
mc alias set majaai http://minio:9000 ${MINIO_ROOT_USER} ${MINIO_ROOT_PASSWORD}
mc mb majaai/documents
mc mb majaai/reports
mc mb majaai/backups

# Set policies
mc policy set download majaai/documents
mc policy set private majaai/reports
mc policy set private majaai/backups

# Enable versioning (for backups)
mc version enable majaai/documents
```

**Storage Structure:**

```
majaai/
├── documents/
│   ├── {user_id}/
│   │   ├── {session_id}/
│   │   │   ├── {timestamp}_{filename}.pdf
│   │   │   ├── {timestamp}_{filename}.xlsx
│   │   │   └── ...
│   │   └── ...
│   └── ...
├── reports/
│   ├── {user_id}/
│   │   ├── {session_id}/
│   │   │   └── report_{timestamp}.pdf
│   │   └── ...
│   └── ...
└── backups/
    ├── postgres/
    │   └── backup_{date}.sql.gz
    ├── chromadb/
    │   └── vectors_{date}.tar.gz
    └── ...
```

---

## 6. Networking & Security

### 🔒 Security Requirements

#### **SSL/TLS Certificates**

```bash
# Option 1: Let's Encrypt (Free, Auto-renewal)
apt-get install certbot python3-certbot-nginx
certbot --nginx -d maja.ai -d www.maja.ai

# Option 2: Self-signed (Development only)
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/ssl/private/maja.key \
    -out /etc/ssl/certs/maja.crt
```

#### **Firewall Configuration (UFW)**

```bash
# Enable UFW
ufw enable

# Allow SSH
ufw allow 22/tcp

# Allow HTTP/HTTPS
ufw allow 80/tcp
ufw allow 443/tcp

# Allow PostgreSQL (internal only)
ufw allow from 10.0.0.0/8 to any port 5432

# Allow Redis (internal only)
ufw allow from 10.0.0.0/8 to any port 6379

# Deny all other incoming
ufw default deny incoming
ufw default allow outgoing
```

#### **Environment Variables (.env)**

```bash
# Application
APP_NAME=MAJA.AI
APP_ENV=production
APP_DEBUG=false
APP_URL=https://maja.ai

# Database
DATABASE_URL=postgresql://majaai:${DB_PASSWORD}@postgres:5432/majaai
DB_PASSWORD=<strong-password-here>

# Redis
REDIS_URL=redis://redis:6379/0

# MinIO
MINIO_ROOT_USER=admin
MINIO_ROOT_PASSWORD=<strong-password-here>
MINIO_ENDPOINT=http://minio:9000
MINIO_BUCKET=documents

# OpenAI
OPENAI_API_KEY=sk-<your-api-key>
OPENAI_MODEL=gpt-4o-mini
OPENAI_MAX_TOKENS=4096
OPENAI_TEMPERATURE=0.3

# Security
SECRET_KEY=<generate-with-openssl-rand-hex-32>
JWT_SECRET_KEY=<generate-with-openssl-rand-hex-32>
JWT_ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=60

# CORS
CORS_ORIGINS=https://maja.ai,https://www.maja.ai

# Upload
MAX_UPLOAD_SIZE_MB=50
ALLOWED_EXTENSIONS=pdf,xlsx,xls,csv

# Rate Limiting
RATE_LIMIT_PER_MINUTE=60
RATE_LIMIT_PER_HOUR=1000
```

---

### 🌐 Nginx Configuration

```nginx
# /etc/nginx/sites-available/maja.ai
upstream frontend {
    server frontend:3000;
}

upstream backend {
    server backend:8000;
}

# HTTP -> HTTPS redirect
server {
    listen 80;
    server_name maja.ai www.maja.ai;
    return 301 https://$server_name$request_uri;
}

# HTTPS server
server {
    listen 443 ssl http2;
    server_name maja.ai www.maja.ai;

    # SSL Configuration
    ssl_certificate /etc/ssl/certs/maja.crt;
    ssl_certificate_key /etc/ssl/private/maja.key;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;

    # Security Headers
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header Referrer-Policy "strict-origin-when-cross-origin" always;

    # Frontend
    location / {
        proxy_pass http://frontend;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_cache_bypass $http_upgrade;
    }

    # Backend API
    location /api/ {
        proxy_pass http://backend;
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        
        # Timeouts for long-running AI requests
        proxy_read_timeout 300s;
        proxy_connect_timeout 75s;
        
        # Request size limits
        client_max_body_size 50M;
    }

    # WebSocket support (for real-time updates)
    location /ws/ {
        proxy_pass http://backend;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
    }

    # Static files caching
    location ~* \.(jpg|jpeg|png|gif|ico|css|js|svg|woff|woff2|ttf|eot)$ {
        proxy_pass http://frontend;
        expires 1y;
        add_header Cache-Control "public, immutable";
    }

    # Gzip compression
    gzip on;
    gzip_vary on;
    gzip_proxied any;
    gzip_comp_level 6;
    gzip_types text/plain text/css text/xml text/javascript application/json application/javascript application/xml+rss;
}
```

---

## 7. Deployment Scenarios

### 📦 Deployment Options

#### **Option 1: Single Server (All-in-One)**

**Pros:**
- ✅ Simple setup
- ✅ Low cost
- ✅ Easy maintenance

**Cons:**
- ❌ Single point of failure
- ❌ Limited scalability
- ❌ Resource contention

**Use Case:** Development, small pemda (<50 users)

**Deployment Steps:**
```bash
# 1. Clone repository
git clone https://github.com/yourorg/maja-ai.git
cd maja-ai

# 2. Configure environment
cp .env.example .env
nano .env  # Edit configuration

# 3. Deploy with Docker Compose
docker-compose up -d

# 4. Initialize database
docker-compose exec backend alembic upgrade head

# 5. Create admin user
docker-compose exec backend python scripts/create_admin.py
```

---

#### **Option 2: Multi-Server (Separated Services)**

**Pros:**
- ✅ Better performance
- ✅ Service isolation
- ✅ Easier troubleshooting

**Cons:**
- ❌ More complex setup
- ❌ Higher cost
- ❌ Requires networking knowledge

**Use Case:** Medium pemda (50-200 users)

**Architecture:**
```
Server 1: Frontend + Backend
Server 2: PostgreSQL + Redis
Server 3: ChromaDB + MinIO
```

---

#### **Option 3: Kubernetes (Cloud Native)**

**Pros:**
- ✅ Auto-scaling
- ✅ High availability
- ✅ Rolling updates
- ✅ Self-healing

**Cons:**
- ❌ Complex setup
- ❌ Requires expertise
- ❌ Higher operational cost

**Use Case:** Large deployment (200+ users), national scale

**Deployment Manifest Example:**

```yaml
# kubernetes/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: maja-ai-backend
  namespace: maja-ai
spec:
  replicas: 3
  selector:
    matchLabels:
      app: maja-ai-backend
  template:
    metadata:
      labels:
        app: maja-ai-backend
    spec:
      containers:
      - name: backend
        image: maja-ai/backend:latest
        ports:
        - containerPort: 8000
        env:
        - name: DATABASE_URL
          valueFrom:
            secretKeyRef:
              name: maja-ai-secrets
              key: database-url
        - name: OPENAI_API_KEY
          valueFrom:
            secretKeyRef:
              name: maja-ai-secrets
              key: openai-api-key
        resources:
          requests:
            memory: "2Gi"
            cpu: "1000m"
          limits:
            memory: "4Gi"
            cpu: "2000m"
        livenessProbe:
          httpGet:
            path: /health
            port: 8000
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /ready
            port: 8000
          initialDelaySeconds: 10
          periodSeconds: 5
---
apiVersion: v1
kind: Service
metadata:
  name: maja-ai-backend
  namespace: maja-ai
spec:
  selector:
    app: maja-ai-backend
  ports:
  - protocol: TCP
    port: 8000
    targetPort: 8000
  type: ClusterIP
---
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: maja-ai-backend-hpa
  namespace: maja-ai
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: maja-ai-backend
  minReplicas: 3
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 80
```

---

## 8. Scalability & Performance

### 📈 Performance Targets

| Metric | Target | Measurement |
|--------|--------|-------------|
| **API Response Time** | < 200ms | p95 latency |
| **Document Upload** | < 5s | for 5MB file |
| **Document Processing** | < 30s | per document |
| **AI Analysis** | < 30s | per request |
| **Concurrent Users** | 100-1000+ | Based on deployment |
| **Database Queries** | < 50ms | p95 latency |
| **Cache Hit Rate** | > 80% | Redis cache |
| **Uptime** | 99.9% | SLA target |

### ⚡ Optimization Strategies

#### **1. Database Optimization**

```sql
-- Add proper indexes
CREATE INDEX CONCURRENTLY idx_documents_session_id ON documents(session_id);
CREATE INDEX CONCURRENTLY idx_analysis_created_at ON analysis_history(created_at DESC);

-- Analyze tables regularly
ANALYZE users, sessions, documents, analysis_history;

-- Vacuum (scheduled weekly)
VACUUM ANALYZE;
```

#### **2. Redis Caching Strategy**

```python
# Cache keys structure
cache_keys = {
    "session:{session_id}": 3600,          # 1 hour
    "user:{user_id}:profile": 1800,        # 30 minutes
    "analysis:{analysis_id}": 7200,        # 2 hours
    "document:{doc_id}:chunks": 86400,     # 24 hours
    "rate_limit:{user_id}": 60,            # 1 minute
}
```

#### **3. CDN Configuration**

```nginx
# Cache static assets
location ~* \.(jpg|jpeg|png|gif|ico|css|js|svg|woff|woff2)$ {
    expires 1y;
    add_header Cache-Control "public, immutable";
    add_header X-Cache-Status $upstream_cache_status;
}
```

#### **4. Connection Pooling**

```python
# SQLAlchemy connection pool
from sqlalchemy import create_engine

engine = create_engine(
    DATABASE_URL,
    pool_size=20,              # Max 20 connections
    max_overflow=10,           # Allow 10 extra under load
    pool_pre_ping=True,        # Test connections before use
    pool_recycle=3600,         # Recycle after 1 hour
)
```

---

## 9. Monitoring & Logging

### 📊 Monitoring Stack

#### **Prometheus Configuration**

```yaml
# prometheus.yml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: 'maja-ai-backend'
    static_configs:
      - targets: ['backend:8000']
    metrics_path: '/metrics'

  - job_name: 'postgres'
    static_configs:
      - targets: ['postgres-exporter:9187']

  - job_name: 'redis'
    static_configs:
      - targets: ['redis-exporter:9121']

  - job_name: 'node'
    static_configs:
      - targets: ['node-exporter:9100']
```

#### **Grafana Dashboards**

**Key Metrics to Monitor:**

1. **Application Metrics:**
   - Request rate (req/s)
   - Response time (p50, p95, p99)
   - Error rate (4xx, 5xx)
   - Active users
   - Document uploads/hour

2. **System Metrics:**
   - CPU usage (%)
   - Memory usage (GB)
   - Disk I/O (MB/s)
   - Network I/O (Mbps)

3. **Database Metrics:**
   - Query latency
   - Connection pool usage
   - Cache hit rate
   - Slow queries

4. **AI/LLM Metrics:**
   - OpenAI API calls/hour
   - Tokens consumed
   - Average response time
   - API errors

---

### 📝 Logging Configuration

#### **Structured Logging (Python)**

```python
# logging_config.py
import logging
import json
from datetime import datetime

class JSONFormatter(logging.Formatter):
    def format(self, record):
        log_obj = {
            "timestamp": datetime.utcnow().isoformat(),
            "level": record.levelname,
            "logger": record.name,
            "message": record.getMessage(),
            "module": record.module,
            "function": record.funcName,
            "line": record.lineno,
        }
        
        if hasattr(record, 'user_id'):
            log_obj["user_id"] = record.user_id
        if hasattr(record, 'session_id'):
            log_obj["session_id"] = record.session_id
            
        if record.exc_info:
            log_obj["exception"] = self.formatException(record.exc_info)
            
        return json.dumps(log_obj)

# Configure logger
logging.basicConfig(
    level=logging.INFO,
    format='%(message)s',
    handlers=[
        logging.FileHandler('/var/log/maja-ai/app.log'),
        logging.StreamHandler()
    ]
)
```

#### **Log Rotation**

```bash
# /etc/logrotate.d/maja-ai
/var/log/maja-ai/*.log {
    daily
    missingok
    rotate 30
    compress
    delaycompress
    notifempty
    create 0640 www-data www-data
    sharedscripts
    postrotate
        systemctl reload nginx
    endscript
}
```

---

## 10. Backup & Disaster Recovery

### 💾 Backup Strategy

#### **Backup Schedule**

| Component | Frequency | Retention | Method |
|-----------|-----------|-----------|--------|
| **PostgreSQL** | Daily (full), Hourly (incremental) | 30 days | pg_dump + WAL archiving |
| **ChromaDB** | Daily | 14 days | Filesystem snapshot |
| **MinIO Objects** | Daily | 30 days | mc mirror |
| **Application Code** | On commit | Indefinite | Git |
| **Configuration** | On change | Indefinite | Git + encrypted secrets |

#### **PostgreSQL Backup Script**

```bash
#!/bin/bash
# /scripts/backup_postgres.sh

BACKUP_DIR="/backups/postgres"
DATE=$(date +%Y%m%d_%H%M%S)
DB_NAME="majaai"

# Create backup directory
mkdir -p $BACKUP_DIR

# Full database dump
pg_dump -U majaai -h postgres -F c -b -v \
    -f $BACKUP_DIR/maja_${DATE}.dump $DB_NAME

# Compress
gzip $BACKUP_DIR/maja_${DATE}.dump

# Upload to remote storage (MinIO/S3)
mc cp $BACKUP_DIR/maja_${DATE}.dump.gz \
    majaai/backups/postgres/

# Remove old local backups (keep 7 days)
find $BACKUP_DIR -name "*.dump.gz" -mtime +7 -delete

# Log backup
echo "$(date) - PostgreSQL backup completed: maja_${DATE}.dump.gz" >> /var/log/maja-ai/backup.log
```

#### **Automated Backup (Cron)**

```cron
# /etc/cron.d/maja-ai-backup

# PostgreSQL full backup (daily at 2 AM)
0 2 * * * root /scripts/backup_postgres.sh

# MinIO objects backup (daily at 3 AM)
0 3 * * * root /scripts/backup_minio.sh

# ChromaDB vector backup (daily at 4 AM)
0 4 * * * root /scripts/backup_chromadb.sh

# Health check (every 5 minutes)
*/5 * * * * root /scripts/health_check.sh
```

---

### 🔄 Disaster Recovery Plan

#### **Recovery Time Objective (RTO):**
- **Critical Services:** < 1 hour
- **Data Services:** < 4 hours
- **Full System:** < 8 hours

#### **Recovery Point Objective (RPO):**
- **Database:** < 1 hour (hourly incremental backups)
- **Documents:** < 24 hours (daily backups)

#### **Recovery Procedures:**

**1. Database Recovery**
```bash
# Restore from latest backup
gunzip /backups/postgres/maja_20240304_020000.dump.gz
pg_restore -U majaai -h postgres -d majaai -c \
    /backups/postgres/maja_20240304_020000.dump
```

**2. Application Recovery**
```bash
# Pull latest stable code
git checkout v1.0.0

# Rebuild containers
docker-compose down
docker-compose build --no-cache
docker-compose up -d

# Verify health
curl http://localhost:8000/health
```

**3. Data Recovery**
```bash
# Restore MinIO objects
mc mirror majaai/backups/documents/ /data/minio/documents/

# Restore ChromaDB
tar -xzf /backups/chromadb/vectors_20240304.tar.gz -C /data/chromadb/
```

---

## 11. Cost Estimation

### 💰 Monthly Cost Breakdown

#### **Scenario 1: Small Deployment (10-50 Users)**

| Item | Spesifikasi | Biaya/Bulan (IDR) |
|------|-------------|-------------------|
| **VPS Application** | 8 vCPU, 32GB RAM | 1,500,000 |
| **VPS Database** | 4 vCPU, 16GB RAM | 800,000 |
| **Storage** | 500 GB SSD | 300,000 |
| **Bandwidth** | 2 TB/month | 200,000 |
| **OpenAI API** | ~1M tokens/month | 500,000 |
| **SSL Certificate** | Let's Encrypt (free) | 0 |
| **Backup Storage** | S3/MinIO 100 GB | 100,000 |
| **Domain & DNS** | .id domain | 50,000 |
| **Monitoring** | Self-hosted | 0 |
| **Total** | | **Rp 3,450,000** |

---

#### **Scenario 2: Medium Deployment (50-200 Users)**

| Item | Spesifikasi | Biaya/Bulan (IDR) |
|------|-------------|-------------------|
| **VPS Load Balancer** | 2 vCPU, 4GB RAM | 400,000 |
| **VPS App Servers (2x)** | 8 vCPU, 32GB RAM each | 3,000,000 |
| **VPS Database** | 8 vCPU, 64GB RAM | 2,500,000 |
| **VPS Storage/Vector** | 8 vCPU, 32GB RAM | 1,500,000 |
| **Storage** | 2 TB SSD | 800,000 |
| **Bandwidth** | 5 TB/month | 500,000 |
| **OpenAI API** | ~5M tokens/month | 2,500,000 |
| **SSL Certificate** | Wildcard cert | 500,000 |
| **Backup Storage** | S3 500 GB | 500,000 |
| **Domain & DNS** | Premium DNS | 200,000 |
| **Monitoring** | Managed (Datadog/NR) | 1,000,000 |
| **Total** | | **Rp 13,400,000** |

---

#### **Scenario 3: Large Deployment (200-1000+ Users)**

| Item | Spesifikasi | Biaya/Bulan (IDR) |
|------|-------------|-------------------|
| **Kubernetes Cluster** | 9 nodes (control + workers) | 25,000,000 |
| **Database Cluster** | PostgreSQL HA (3 nodes) | 10,000,000 |
| **Object Storage Cluster** | MinIO HA (4 nodes) | 8,000,000 |
| **Storage** | 10 TB SSD/NVMe | 5,000,000 |
| **Bandwidth** | 20 TB/month | 2,000,000 |
| **OpenAI API** | ~20M tokens/month | 10,000,000 |
| **SSL Certificates** | Enterprise | 1,000,000 |
| **Backup & DR** | Multi-region | 3,000,000 |
| **Domain & DNS** | Enterprise DNS | 500,000 |
| **Monitoring & APM** | Full stack (Datadog) | 5,000,000 |
| **Security** | WAF, DDoS protection | 2,000,000 |
| **DevOps Support** | On-call engineer | 15,000,000 |
| **Total** | | **Rp 86,500,000** |

---

### 💡 Cost Optimization Tips

1. **OpenAI API:**
   - Gunakan `gpt-4o-mini` untuk development (lebih murah)
   - Implementasi caching untuk queries yang sering diulang
   - Batasi `max_tokens` per request
   - Gunakan prompt engineering untuk response yang lebih ringkas

2. **Compute Resources:**
   - Auto-scaling pada Kubernetes untuk adjust dengan beban
   - Gunakan spot instances untuk non-critical workloads
   - Shutdown dev/test environments di luar jam kerja

3. **Storage:**
   - Lifecycle policies untuk archived data (move ke cold storage)
   - Compress backup files
   - Deduplikasi dokumen yang sama

4. **Bandwidth:**
   - Enable CDN untuk static assets
   - Compress responses (gzip/brotli)
   - Optimize images dan documents sebelum upload

---

## 📚 Summary Checklist

### ✅ Pre-Deployment Checklist

- [ ] **Hardware:** Server specs meet minimum requirements
- [ ] **OS:** Ubuntu 22.04 LTS or Rocky Linux 9 installed
- [ ] **Network:** Firewall configured, SSL certificate ready
- [ ] **Docker:** Docker & Docker Compose installed
- [ ] **Database:** PostgreSQL initialized with schema
- [ ] **Storage:** MinIO configured with buckets
- [ ] **Secrets:** All environment variables set securely
- [ ] **Backup:** Automated backup scripts scheduled
- [ ] **Monitoring:** Prometheus & Grafana configured
- [ ] **Logging:** Log rotation and centralized logging setup
- [ ] **Testing:** Load testing completed successfully

### ✅ Post-Deployment Checklist

- [ ] **Health Check:** All services responding to /health endpoint
- [ ] **SSL:** HTTPS working, certificate valid
- [ ] **Performance:** API response times within SLA
- [ ] **Monitoring:** Alerts configured and tested
- [ ] **Backup:** First backup completed and verified
- [ ] **Documentation:** Runbook and SOP documented
- [ ] **Training:** Team trained on deployment and operations
- [ ] **Support:** On-call rotation established

---

<div align="center">

## 🏛️ MAJA.AI — Production Ready Infrastructure

**Scalable** | **Secure** | **Reliable** | **Government-Grade**

*Infrastruktur yang dirancang untuk mendukung transformasi digital pemerintahan Indonesia*

---

**Dokumentasi Lengkap ✅**

</div>
