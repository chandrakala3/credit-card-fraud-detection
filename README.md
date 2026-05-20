# 💳 Credit Card Fraud Detection System

[![Platform](https://img.shields.io/badge/Platform-React%20%7C%20FastAPI-blue?style=for-the-badge)](https://github.com/chandrakala3/credit-card-fraud-detection)
[![ML](https://img.shields.io/badge/ML-Random%20Forest-orange?style=for-the-badge)](https://github.com/chandrakala3/credit-card-fraud-detection)
[![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)](https://github.com/chandrakala3/credit-card-fraud-detection)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](https://github.com/chandrakala3/credit-card-fraud-detection)

> **Final Year Project** — B.Tech in Computer Science Engineering

---

## 📌 Project Overview

Credit card fraud is one of the fastest-growing threats in digital banking, causing billions in losses globally every year. Traditional rule-based systems fail to adapt to individual user behavior, resulting in missed fraud and excessive false alerts.

This project presents **DetectAI** — a full-stack AI-powered web application that detects fraudulent credit card transactions in **real time** using a **Random Forest machine learning model**. The system analyzes each transaction against the user's personal spending baseline and instantly classifies it as **Safe**, **Suspicious**, or **Fraudulent**, along with a deviation score.

The application features two separate portals — a **Card Holder Dashboard** for users to monitor their transactions and alerts, and an **Admin Control Panel** for administrators to manage users, view all transactions, and retrain the ML model live.

---

## 🎯 Objectives

- Detect fraudulent transactions in real time using a trained ML model
- Calculate a **deviation score** per transaction based on each user's average spending
- Provide card holders with instant fraud alerts and transaction history
- Give administrators full visibility and ML model control via a dedicated panel
- Support **live model retraining** using real accumulated transaction data

---

## 🏗️ System Architecture

```
User (Browser)
       │
       ▼
React + Vite Frontend
       │
       ▼
FastAPI Backend (Python)
       │
    ┌──┴──────────────┐
    │                 │
    ▼                 ▼
SQLite Database   Random Forest ML Model
(SQLAlchemy ORM)  (scikit-learn .pkl)
                       │
                       ▼
            Fraud Probability Score
            + Risk Label (Safe / Suspicious / Fraud)
            + Deviation Score
```

---

## 🚀 Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 18, Vite 5, Tailwind CSS |
| UI Library | shadcn/ui, Radix UI, Lucide React |
| Charts | Recharts |
| Animations | Framer Motion |
| Forms | React Hook Form + Zod |
| HTTP Client | Axios, TanStack Query |
| Backend | FastAPI 0.104, Uvicorn |
| Database | SQLite, SQLAlchemy 2.0 |
| ML Model | Random Forest — scikit-learn 1.3 |
| Validation | Pydantic 2.5 |
| Security | Passlib + bcrypt |

---

## 🔧 Features

### 👤 Card Holder Portal
- Personal dashboard with total, suspicious & fraudulent transaction counts
- Full transaction history with risk labels and deviation scores
- **Transaction Simulator** — enter amount, location, device, mode and instantly get ML prediction
- Fraud alerts page with notification count
- Report wrong predictions for model feedback
- Secure registration with monthly income and daily spending limit
- Auto-seeded transaction history on registration (10 baseline transactions)

### 🛡️ Admin Control Panel
- Risk score distribution pie chart (Safe / Suspicious / Fraudulent)
- All card holders overview with spending analytics
- Full transaction log across all users with deviation scores and timestamps
- **Train ML Model** — retrain Random Forest on real accumulated data
- **Trigger High Risk Transaction** — inject a test fraud transaction for any user

---

## 🤖 ML Model Details

| Detail | Info |
|--------|------|
| Algorithm | Random Forest Classifier |
| Estimators | 100 decision trees |
| Max Depth | 10 |
| Class Weighting | Balanced (handles fraud-normal imbalance) |
| Training Data | 5,000 synthetic transactions (92% normal, 8% fraud) |
| Features | Amount, Deviation Score, Location, Device, Mode, Hour of Day |
| Model File | `fraud_model_v1.pkl` (auto-saved, reloaded on restart) |
| Retraining | Live via Admin Panel (minimum 100 real transactions) |

**Risk Thresholds:**

| Deviation Score | Risk Label |
|----------------|-----------|
| Below 1.5x avg spending | Safe |
| 1.5x – 2.5x avg spending | Suspicious |
| Above 2.5x avg spending | Flagged / Fraud |

---

## 📁 Project Structure

```
credit-card-fraud-detection/
├── Source Code/
│   ├── backend/
│   │   ├── main.py              # FastAPI app + all API routes
│   │   ├── ml_engine.py         # RandomForest model class
│   │   ├── simulator.py         # Transaction simulator & history seeder
│   │   ├── crud.py              # Database CRUD operations
│   │   ├── models.py            # SQLAlchemy ORM models
│   │   ├── schemas.py           # Pydantic request/response schemas
│   │   ├── database.py          # DB connection & session management
│   │   ├── config.py            # App configuration & risk thresholds
│   │   ├── models/
│   │   │   └── fraud_model_v1.pkl
│   │   └── requirements.txt
│   └── frontend/
│       ├── src/
│       │   ├── components/
│       │   │   ├── dashboard/
│       │   │   │   ├── AdminDashboard.jsx
│       │   │   │   ├── UserDashboard.jsx
│       │   │   │   ├── RiskDistributionChart.jsx
│       │   │   │   └── TransactionSimulator.jsx
│       │   │   └── ui/           # shadcn/ui components
│       │   ├── pages/
│       │   │   ├── Dashboard.jsx
│       │   │   ├── Login.jsx
│       │   │   ├── Register.jsx
│       │   │   ├── Alerts.jsx
│       │   │   └── Portfolio.jsx
│       │   ├── lib/
│       │   │   ├── api.js
│       │   │   └── utils.js
│       │   └── App.jsx
│       ├── package.json
│       └── vite.config.js
└── Documents/
    ├── Credit Card Fraud Detection - Documentation.pdf
    ├── Credit Card Fraud Detection System - QnAs.pdf
    └── Setup.pdf
```

---

## ⚙️ Setup & Installation

### 1. Clone the Repository

```bash
git clone https://github.com/chandrakala3/credit-card-fraud-detection.git
cd "credit-card-fraud-detection/Source Code"
```

### 2. Backend Setup

```bash
cd backend

# Create and activate virtual environment
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # Mac/Linux

# Install dependencies
pip install -r requirements.txt

# Run the backend server
python main.py
```

Backend runs at: `http://localhost:8000`  
API docs at: `http://localhost:8000/docs`

> On first run, the ML model auto-trains on 5,000 synthetic transactions and saves to `models/fraud_model_v1.pkl`

### 3. Frontend Setup

```bash
cd frontend

npm install
npm run dev
```

Frontend runs at: `http://localhost:8081`

### 4. Open Application

```
http://localhost:8081
```

---

## 📡 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/users/register` | Register new card holder |
| POST | `/users/login` | Card holder login |
| GET | `/users/{user_id}` | Get user profile |
| GET | `/transactions/{user_id}` | Get user transactions |
| POST | `/transactions/simulate` | Simulate & predict a transaction |
| POST | `/transactions/report` | Report a wrong prediction |
| GET | `/alerts/{user_id}` | Get fraud alerts |
| POST | `/admin/login` | Admin login |
| GET | `/admin/users` | Get all card holders |
| GET | `/admin/transactions` | Get all transactions |
| GET | `/admin/analytics/summary` | Risk distribution summary |
| POST | `/admin/train` | Retrain the ML model |
| POST | `/admin/trigger-high-risk` | Trigger a test high-risk transaction |

---

## 🔐 Login Credentials

| Role | Username / Email | Password |
|------|------------------|----------|
| Admin | admin | admin123 |
| Card Holder | Register via app | — |

---

## 📈 Results

- Real-time ML predictions delivered instantly on transaction simulation
- Deviation score correctly identifies anomalous spending patterns
- Admin panel updates risk distribution chart dynamically
- Model retraining supported live without code changes
- Auto-seeded transaction history establishes accurate user spending baseline on registration

---

## 🌱 Applications

- Personal credit card fraud monitoring
- Banking and fintech fraud detection systems
- Financial security dashboards
- Academic demonstration of ML in real-world applications
- Foundation for enterprise-grade fraud detection platforms

---

## 🔮 Future Scope

- JWT-based authentication (replacing hardcoded admin token)
- Deep Learning models (LSTM, Autoencoders) for higher accuracy
- Email / SMS alerts on fraud detection
- Cloud deployment (AWS / Azure / GCP)
- Real-time streaming with Apache Kafka
- Mobile app (Android/iOS) with push notifications

---

## 📄 License

This project is licensed under the **MIT License**.

---

## 🙏 Acknowledgements

Special thanks to the open-source community and the developers of FastAPI, React, scikit-learn, and shadcn/ui for making this project possible.

---

Made with ❤️ by [chandrakala3](https://github.com/chandrakala3)

