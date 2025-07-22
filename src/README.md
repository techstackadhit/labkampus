# LabKampus 

**LabKampus** adalah platform web terintegrasi untuk praktikum mahasiswa berbasis container. Sistem ini memungkinkan mahasiswa menjalankan lab secara mandiri melalui web, dengan environment yang otomatis disiapkan menggunakan Docker dan Kubernetes.

---

## Fitur Utama

- Autentikasi mahasiswa, asisten, dan admin (Email/SSO)
- Modul praktikum interaktif dengan dukungan Markdown
- Eksekusi lab environment berbasis Docker container
- Isolasi tiap user: 1 user = 1 pod = 1 container
- Monitoring via Prometheus + Grafana
- Submit file/kode, dengan auto-checker script
- CI/CD pipeline via GitHub Actions

---

## Arsitektur

```bash
[Frontend React]
│
▼
/api
│
▼
[Backend FastAPI]
├──→ [Kubernetes API] → [Lab Container per Mahasiswa]
├──→ [PostgreSQL]
└──→ [Monitoring Stack (Prometheus, Grafana)]
```

Keterangan:
- **Frontend** mengakses backend melalui endpoint `/api`.
- **Backend** mengelola autentikasi, modul, dan memicu eksekusi lab container via Kubernetes.
- **PostgreSQL** menyimpan data pengguna, modul, dan hasil praktikum.
- **Monitoring Stack** seperti Prometheus dan Grafana menerima metrik dari container dan backend untuk keperluan observabilitas.

note:
- Semua komponen bisa dijalankan lokal (minikube) atau on-prem (VM Proxmox).
- Komunikasi internal antar komponen menggunakan REST + pod networking.
- Skema akses mahasiswa: via LAN kampus atau WireGuard VPN (opsional).

---

## Stack Teknologi

| Layer        | Tools                         |
|--------------|-------------------------------|
| Frontend     | React + Tailwind CSS          |
| Backend API  | FastAPI (Python)              |
| Database     | PostgreSQL                    |
| Container    | Docker                        |
| Orchestration| Kubernetes (minikube/k3s)     |
| Provisioning | Terraform                     |
| Automation   | Ansible                       |
| Monitoring   | Prometheus + Grafana          |
| CI/CD        | GitHub Actions                |
| API Testing  | Postman                       |

---

## Cara Menjalankan Lokal (Dev)

### 1. Clone Repo

```bash
git clone https://github.com/username/labkampus.git
cd labkampus
```

### 2. Jalankan Backend
```
cd backend
python -m venv venv
venv\Scripts\activate  # Windows
pip install -r requirements.txt
uvicorn app.main:app --reload
```

### 3. Jalankan Frontend
```
cd frontend
npm install
npm run dev
```

### 4. Docker Compose (opsional)
```
docker-compose up --build
```

## Testing
- Jalankan tes backend: pytest
- Koleksi Postman tersedia di folder /postman

## Struktur Folder
```
labkampus/
├── frontend/        # React + Tailwind UI
├── backend/         # FastAPI app
├── infra/           # Kubernetes, Terraform, Ansible
├── monitoring/      # Prometheus, Grafana config
├── scripts/         # Helper scripts
├── docs/            # Dokumen arsitektur, ERD, dll
├── postman/         # API collection
└── .github/         # CI/CD workflows
```

## Roadmap Singkat
- Setup backend API dasar (auth, modul, user)
- Integrasi frontend + backend
- Deploy ke Kubernetes
- Tambah monitoring dan logging
- Finalisasi fitur submit dan evaluasi otomatis

## Kontribusi
Walau proyek ini solo-dev friendly, pull request dan masukan tetap terbuka!
1. Fork repo ini
2. Buat branch baru: feature/nama-fitur
3. Commit perubahan
4. Buka Pull Request ke dev

## Lisensi
Open Source — MIT License

## Kontak
Pengembang: [Nama Kamu]
Email: namakamu@example.com
GitHub: github.com/username


