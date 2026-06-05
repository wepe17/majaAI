# 📊 MAJA.AI — Infrastruktur Quick Reference

**Ringkasan Kebutuhan Infrastruktur untuk Decision Makers**

---

## 🎯 Pilihan Deployment (Quick Comparison)

| Aspek | Small | Medium | Large | Enterprise |
|-------|-------|--------|-------|------------|
| **Users** | 10-50 | 50-200 | 200-1000 | 1000+ |
| **Use Case** | 1 Pemda Kecil | Multi-Pemda | Provinsi | Nasional |
| **Servers** | 2 VPS | 4 VPS | Kubernetes (9+ nodes) | K8s Cluster HA |
| **CPU Total** | 12 vCPU | 28 vCPU | 144+ vCPU | 300+ vCPU |
| **RAM Total** | 48 GB | 144 GB | 640+ GB | 1.5+ TB |
| **Storage** | 1.5 TB | 6 TB | 16 TB | 50+ TB |
| **Monthly Cost** | Rp 3.5 juta | Rp 13 juta | Rp 86 juta | Rp 200+ juta |
| **Setup Time** | 1-2 hari | 3-5 hari | 2-3 minggu | 1-2 bulan |
| **Team Required** | 1-2 orang | 2-3 orang | 4-6 orang | 10+ orang |

---

## 🏗️ Arsitektur Sistem (High Level)

```
┌─────────────┐
│   USERS     │ Web Browser
└──────┬──────┘
       │ HTTPS
       ↓
┌─────────────────────────────────────┐
│     FRONTEND (Next.js/React)        │ Presentation
├─────────────────────────────────────┤
│     BACKEND API (FastAPI)           │ Application
├─────────────────────────────────────┤
│  AI SERVICES (LangChain + OpenAI)   │ Intelligence
├─────────────────────────────────────┤
│  PostgreSQL | ChromaDB | Redis      │ Data Layer
│  MinIO Object Storage               │
└─────────────────────────────────────┘
```

---

## 💻 Technology Stack Summary

### Frontend
- **Framework:** Next.js 14 / React 18
- **Styling:** Tailwind CSS
- **Charts:** Chart.js
- **Deployment:** Docker / Vercel

### Backend
- **Framework:** Python FastAPI
- **Server:** Uvicorn (ASGI)
- **API:** RESTful + WebSocket
- **Auth:** JWT + OAuth2

### AI/ML
- **LLM:** OpenAI GPT-4o / GPT-4o-mini
- **RAG:** LangChain
- **Embeddings:** OpenAI text-embedding-3-small
- **Vector DB:** ChromaDB

### Data
- **Primary DB:** PostgreSQL 16
- **Cache:** Redis 7
- **Object Storage:** MinIO / S3
- **Backup:** pg_dump + rsync

### Infrastructure
- **Container:** Docker + Docker Compose
- **Orchestration:** Kubernetes (optional)
- **Reverse Proxy:** Nginx
- **Monitoring:** Prometheus + Grafana
- **Logging:** ELK Stack

---

## 📦 Deployment Scenarios

### Scenario 1: Single Server (Recommended for Start)

**Hardware:**
- 1 server: 8 vCPU, 32 GB RAM, 1 TB SSD
- Cost: ~Rp 1.5 juta/bulan

**Services:**
- Frontend + Backend + PostgreSQL + Redis + ChromaDB + MinIO

**Deployment:**
```bash
git clone https://github.com/yourorg/maja-ai.git
cd maja-ai
docker-compose up -d
```

**Pros:** Simple, low cost, easy maintenance  
**Cons:** Single point of failure, limited scaling

---

### Scenario 2: Multi-Server (Recommended for Production)

**Hardware:**
- Server 1: App (8 vCPU, 32 GB, 500 GB) — Frontend + Backend
- Server 2: DB (8 vCPU, 64 GB, 2 TB) — PostgreSQL
- Server 3: AI (8 vCPU, 32 GB, 4 TB) — ChromaDB + MinIO
- Server 4: LB (2 vCPU, 4 GB, 100 GB) — Nginx

**Cost:** ~Rp 10-15 juta/bulan

**Pros:** Better performance, fault isolation, scalable  
**Cons:** More complex setup, networking knowledge required

---

### Scenario 3: Kubernetes (Recommended for Scale)

**Hardware:**
- 3 control plane nodes: 4 vCPU, 16 GB each
- 6+ worker nodes: 16 vCPU, 64 GB each
- 3 database nodes: 16 vCPU, 128 GB each

**Cost:** ~Rp 50-100 juta/bulan

**Pros:** Auto-scaling, HA, self-healing, rolling updates  
**Cons:** Complex, requires K8s expertise, high operational cost

---

## 💰 Cost Breakdown (Monthly)

### Small Deployment (10-50 Users)

| Item | Cost |
|------|------|
| 2x VPS Cloud | Rp 2,300,000 |
| Storage 500 GB | Rp 300,000 |
| Bandwidth 2 TB | Rp 200,000 |
| OpenAI API (~1M tokens) | Rp 500,000 |
| Backup Storage | Rp 100,000 |
| Domain & SSL | Rp 50,000 |
| **Total** | **Rp 3,450,000** |

### Medium Deployment (50-200 Users)

| Item | Cost |
|------|------|
| 4x VPS Cloud | Rp 7,400,000 |
| Storage 2 TB | Rp 800,000 |
| Bandwidth 5 TB | Rp 500,000 |
| OpenAI API (~5M tokens) | Rp 2,500,000 |
| Backup & SSL | Rp 1,000,000 |
| Monitoring Tools | Rp 1,000,000 |
| Domain & Premium DNS | Rp 200,000 |
| **Total** | **Rp 13,400,000** |

### Large Deployment (200-1000+ Users)

| Item | Cost |
|------|------|
| Kubernetes Cluster | Rp 25,000,000 |
| Database HA Cluster | Rp 10,000,000 |
| Storage Cluster | Rp 8,000,000 |
| Storage 10 TB | Rp 5,000,000 |
| Bandwidth 20 TB | Rp 2,000,000 |
| OpenAI API (~20M tokens) | Rp 10,000,000 |
| Monitoring & Security | Rp 8,000,000 |
| Backup & DR | Rp 3,000,000 |
| DevOps Support | Rp 15,000,000 |
| **Total** | **Rp 86,000,000** |

---

## 🔒 Security Essentials

### Must-Have Security Features

- ✅ **SSL/TLS Certificates** (HTTPS everywhere)
- ✅ **Firewall** (UFW/iptables configured)
- ✅ **JWT Authentication** (secure API access)
- ✅ **Rate Limiting** (prevent abuse)
- ✅ **Input Validation** (prevent injection attacks)
- ✅ **Encrypted Secrets** (environment variables)
- ✅ **Audit Logging** (track user activities)
- ✅ **Regular Backups** (automated daily backups)
- ✅ **Intrusion Detection** (fail2ban, OSSEC)
- ✅ **Security Updates** (automated patching)

---

## 📊 Performance Targets

| Metric | Target |
|--------|--------|
| **API Response Time** | < 200ms (p95) |
| **Document Upload** | < 5 seconds (5MB file) |
| **AI Analysis** | < 30 seconds |
| **Page Load Time** | < 2 seconds |
| **Concurrent Users** | 100-1000+ |
| **Uptime SLA** | 99.9% (8.76 hours downtime/year) |
| **Database Query** | < 50ms (p95) |
| **Cache Hit Rate** | > 80% |

---

## 💾 Backup & Recovery

### Backup Schedule

| Component | Frequency | Retention |
|-----------|-----------|-----------|
| **PostgreSQL** | Daily (full) + Hourly (incremental) | 30 days |
| **Documents** | Daily | 30 days |
| **Vector DB** | Daily | 14 days |
| **Config** | On change | Indefinite |

### Recovery Objectives

- **RTO (Recovery Time Objective):** < 4 hours
- **RPO (Recovery Point Objective):** < 1 hour (data loss tolerance)

---

## 🚀 Quick Start Commands

### Development Setup
```bash
# Clone repository
git clone https://github.com/yourorg/maja-ai.git
cd maja-ai

# Configure environment
cp .env.example .env
nano .env

# Start services
docker-compose up -d

# Initialize database
docker-compose exec backend alembic upgrade head

# Create admin user
docker-compose exec backend python scripts/create_admin.py

# Access application
open http://localhost:3000
```

### Production Deployment
```bash
# Pull latest code
git pull origin main

# Build images
docker-compose -f docker-compose.prod.yml build

# Deploy
docker-compose -f docker-compose.prod.yml up -d

# Health check
curl https://maja.ai/api/health
```

### Backup & Restore
```bash
# Backup database
./scripts/backup_postgres.sh

# Restore database
pg_restore -U majaai -d majaai backup_file.dump

# Backup files
./scripts/backup_minio.sh
```

---

## 📋 Deployment Checklist

### Pre-Deployment

- [ ] Server provisioned and accessible
- [ ] Domain purchased and DNS configured
- [ ] SSL certificate obtained
- [ ] Docker & Docker Compose installed
- [ ] Environment variables configured
- [ ] Firewall rules configured
- [ ] OpenAI API key obtained
- [ ] Backup storage configured

### Post-Deployment

- [ ] All services healthy (`docker-compose ps`)
- [ ] HTTPS working (certificate valid)
- [ ] Database migrations applied
- [ ] Admin user created
- [ ] Backups tested and working
- [ ] Monitoring dashboards accessible
- [ ] Load testing completed
- [ ] Documentation updated

---

## 👥 Team Requirements

### Small Deployment
- **1 DevOps Engineer** (setup & maintenance)
- **1 Developer** (customization & support)
- **Part-time** commitment (10-20 hours/month)

### Medium Deployment
- **1 DevOps Engineer** (infrastructure)
- **1 Backend Developer** (API & services)
- **1 Frontend Developer** (UI/UX)
- **Part-time** to **Full-time**

### Large Deployment
- **2 DevOps Engineers** (infrastructure & security)
- **2 Backend Developers** (API development)
- **2 Frontend Developers** (UI/UX)
- **1 Data Engineer** (database & analytics)
- **1 Security Engineer** (security & compliance)
- **1 QA Engineer** (testing)
- **Full-time** team

---

## 📞 Support & Maintenance

### Included Services

- ✅ Bug fixes and patches
- ✅ Security updates
- ✅ Performance optimization
- ✅ Documentation updates
- ✅ Email support (business hours)

### Optional Services (Additional Cost)

- 💼 24/7 On-call support
- 💼 Custom feature development
- 💼 Training & workshops
- 💼 Managed services
- 💼 SLA guarantees

---

## 📚 Documentation Links

- **Full Infrastructure Guide:** [INFRASTRUCTURE.md](./INFRASTRUCTURE.md)
- **API Documentation:** [API.md](./API.md)
- **Deployment Guide:** [DEPLOYMENT.md](./DEPLOYMENT.md)
- **Security Guide:** [SECURITY.md](./SECURITY.md)
- **Troubleshooting:** [TROUBLESHOOTING.md](./TROUBLESHOOTING.md)

---

<div align="center">

## 🏛️ MAJA.AI Infrastructure

**Siap Deploy dalam Hitungan Hari**

**Dokumentasi Lengkap** | **Support Professional** | **Government-Grade**

---

*Untuk konsultasi infrastruktur lebih lanjut, hubungi tim technical support*

</div>
