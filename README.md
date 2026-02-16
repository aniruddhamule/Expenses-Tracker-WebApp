# 💰 Expenses Tracker WebApp – Dockerized on AWS EC2

## 📌 Project Overview

This project is a production-style Expenses Tracker Web Application deployed on AWS EC2 using Docker and Docker Compose.

The application follows a multi-container architecture:
- **Nginx** - Reverse proxy and static file server
- **WebApp** - Application server (Python/Flask/Django)
- **Database** - Persistent data storage (PostgreSQL/MySQL)
- **Docker Network** - Internal container communication
- **AWS EC2** - Cloud infrastructure host

---

## 🏗 Architecture Diagram

*<img width="2816" height="1536" alt="Gemini_Generated_Image_qwdahbqwdahbqwda" src="https://github.com/user-attachments/assets/646b3bed-791b-4c75-a2f1-e8fbd30cc78c" />*

---

## ⚙️ How This Project Works (Step-by-Step)

### 1️⃣ User Request Flow

1. User hits EC2 Public IP in browser.
2. Request reaches EC2 instance.
3. Port 80 is exposed via Docker.
4. Nginx container receives request.
5. Nginx forwards request to WebApp container.
6. WebApp processes business logic (expense tracking).
7. WebApp communicates with Database container.
8. Response flows back to user.

---

## ☁ AWS EC2 Setup

### 1️⃣ Connect to EC2

```bash
ssh -i your-key.pem ubuntu@<EC2_PUBLIC_IP>
```

### 2️⃣ Install Docker

```bash
sudo apt update -y
sudo apt install docker.io -y
docker --version
sudo systemctl start docker
sudo systemctl enable docker
```

### 3️⃣ Install Docker Compose

```bash
sudo apt install docker-compose -y
```

Verify:

```bash
docker compose version
```

---

## 📦 Clone Repository

```bash
git clone https://github.com/aniruddhamule/Expenses-Tracker-WebApp.git
cd Expenses-Tracker-WebApp
```

---

## 🐳 Build & Run Application

```bash
docker compose up --build -d
```

**What This Command Does:**

- Builds WebApp image
- Builds Nginx image (if applicable)
- Pulls Database image (PostgreSQL/MySQL)
- Creates Docker network
- Creates volumes for data persistence
- Starts all containers

---

## 🔍 Verify Containers

```bash
docker ps
```

**Expected containers:**

- `nginx_cont` (or nginx service)
- `webapp_cont` (or app service)
- `db_cont` (database service)

---

## 📊 Check Container Logs

### Nginx Logs (if using Nginx)
```bash
docker logs nginx_cont
```

### WebApp Logs
```bash
docker logs webapp_cont
```

### Database Logs
```bash
docker logs db_cont
```

---

## 🌐 Access Application

Open in browser:

```
http://<EC2_PUBLIC_IP>
```

---

## 💰 Application Features

- ✅ Add daily expenses with categories
- ✅ View expense history
- ✅ Filter expenses by date/category
- ✅ Visual charts for spending analysis
- ✅ Monthly budget tracking
- ✅ Export reports (CSV/PDF)

---

## 🐳 Docker Networking Explanation

Docker Compose automatically creates a bridge network.

Containers communicate using service names defined in `docker-compose.yml`.

**Example:**

WebApp connects to Database using:

```
DB_HOST=db_cont
DB_NAME=expenses_db
DB_USER=postgres
DB_PASSWORD=your_password
```

Nginx forwards traffic to:

```
webapp_cont:5000  (or whatever port your app uses)
```

Database is NOT publicly exposed.

---

## 🗄 Database Persistence

Database uses a Docker volume:

```
expenses-data/
```

This ensures expense data is not lost when containers restart.

---

## 🔁 Restart / Rebuild Application

If code changes:

```bash
docker compose down
docker compose up --build -d
```

---

## 🛑 Stop Application

```bash
docker compose down
```

---

## 📁 Project Structure

```
Expenses-Tracker-WebApp/
├── app/
│   ├── static/
│   ├── templates/
│   ├── __init__.py
│   ├── models.py
│   ├── routes.py
│   └── utils.py
├── nginx/
│   ├── Dockerfile
│   └── nginx.conf
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
└── README.md
```

---

## 📸 Application Screenshots

### 📝 Dashboard View
*<img width="1357" height="768" alt="Screenshot 2026-02-15 022706" src="https://github.com/user-attachments/assets/73c59585-444f-44fb-9650-f1ec1306fe31" />
*

---

### 📊 logs
*<img width="1360" height="642" alt="Screenshot 2026-02-15 022724" src="https://github.com/user-attachments/assets/0694aecb-2c72-49a4-9dcc-5e518b3cfb18" />*

---

### ☁ AWS EC2 Instance Running
*<img width="1360" height="624" alt="Screenshot 2026-02-15 022642" src="https://github.com/user-attachments/assets/6369aa55-8c08-4d1d-9017-65d30ec53e03" />*

---

## 🎯 Key Features

- ✅ Multi-container Docker architecture
- ✅ Nginx reverse proxy (if applicable)
- ✅ Web application with expense tracking
- ✅ Database with persistent storage
- ✅ Deployed on AWS EC2
- ✅ Production-ready setup
- ✅ Data visualization for expenses

---

## 📝 Technologies Used

- **Backend:** Python/Flask or Django
- **Frontend:** HTML, CSS, JavaScript, Bootstrap
- **Database:** PostgreSQL/MySQL/SQLite
- **Web Server:** Nginx
- **Containerization:** Docker, Docker Compose
- **Cloud:** AWS EC2
- **Version Control:** Git/GitHub
- **Charts:** Chart.js/Matplotlib

---

## 🚨 Troubleshooting

### Container not starting?
```bash
docker logs <container_name>
```

### Database connection issues?
Check `docker-compose.yml` environment variables:

- `DB_HOST`
- `DB_PORT`
- `DB_NAME`
- `DB_USER`
- `DB_PASSWORD`

---

## 📋 Environment Variables

Create a `.env` file for sensitive data:

```env
DB_NAME=expenses_db
DB_USER=postgres
DB_PASSWORD=secure_password
DB_HOST=db_cont
SECRET_KEY=your_secret_key
```

---

## 🔒 Security Best Practices

- ✅ Database not exposed to public internet
- ✅ Environment variables for sensitive data
- ✅ Nginx handles public traffic
- ✅ Regular security updates
- ✅ Volume permissions properly set

---


## 📊 Quick Reference Commands

| Command | Description |
|---------|-------------|
| `docker compose up --build -d` | Build and start all containers |
| `docker compose down` | Stop all containers |
| `docker compose down -v` | Stop and remove volumes (⚠️ deletes data) |
| `docker ps` | List running containers |
| `docker logs -f webapp_cont` | Follow webapp logs |
| `docker exec -it webapp_cont bash` | Access container shell |
| `docker system prune -a` | Clean up unused Docker resources |

---

## ✅ Deployment Checklist

- [ ] AWS EC2 instance created
- [ ] Security group configured (ports 22, 80)
- [ ] Docker and Docker Compose installed
- [ ] Repository cloned
- [ ] Environment variables configured
- [ ] Docker images built successfully
- [ ] All containers running
- [ ] Application accessible via browser
- [ ] Database initialized
- [ ] Can add/view expenses

---

## Credits & Acknowledgments

This project is based on the original work by **Shubham Londhe** 

Original Repository: (https://github.com/LondheShubham153/django-notes-app.git)

I have used this project for learning and deployment purposes, with modifications for AWS EC2 deployment and Docker containerization.

---
