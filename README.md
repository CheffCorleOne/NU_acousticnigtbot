# 🎸 Acoustic Night --- Telegram Collaboration Bot

A Telegram bot that helps musicians create profiles, find collaborators,
and connect after a mutual match.\
Built with **Python**, **python-telegram-bot**, and **PostgreSQL
(JSONB)**.

## ✨ Features

-   **Create & edit a musician profile**
    -   Choose instruments you play
    -   Choose instruments you are seeking
    -   Short bio (max 120 characters)
-   **Two search modes**
    -   🎯 **Smart Matches** --- mutual instrument interest
    -   🔀 **Browse All** --- swipe-style browsing
-   **Collaboration requests**
    -   Send a "Let's Collab" request\
    -   Other user gets **Accept / Decline**
    -   Contact becomes visible **only** after mutual match
-   **Built-in Health Check Server** for hosting platforms.

## 🗂 Tech Stack

-   Python 3.10+
-   python-telegram-bot v20.6
-   PostgreSQL (JSONB)
-   psycopg2

## 🚀 Installation

``` bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO
python3 -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install -r requirements.txt
```

## 🔧 Environment Variables

    TELEGRAM_BOT_TOKEN=123456:ABC...
    DATABASE_URL=postgres://USER:PASSWORD@HOST:5432/DBNAME
    PORT=10000

## 🗄 Database (JSONB)

``` sql
CREATE TABLE IF NOT EXISTS users (
    user_id TEXT PRIMARY KEY,
    data JSONB NOT NULL
);
```

Example profile:

``` json
{
  "user_id": "123",
  "name": "John",
  "username": "john",
  "instruments": ["guitarist"],
  "seeking": ["vocalist"],
  "bio": "Looking for vocalist",
  "matches": [],
  "pending": [],
  "created_at": "2025-01-12T10:20:54"
}
```

## ▶️ Running

``` bash
python main.py
```

## 🔄 systemd Service Example

    [Unit]
    Description=Acoustic Night Telegram Bot
    After=network.target

    [Service]
    User=ubuntu
    WorkingDirectory=/home/ubuntu/YOUR_REPO
    Environment="TELEGRAM_BOT_TOKEN=YOUR_TOKEN"
    Environment="DATABASE_URL=postgres://USER:PASS@HOST/DB"
    ExecStart=/home/ubuntu/YOUR_REPO/venv/bin/python main.py
    Restart=always

    [Install]
    WantedBy=multi-user.target

## 🐳 Dockerfile

    FROM python:3.11-slim
    WORKDIR /app
    COPY . .
    RUN pip install --upgrade pip && pip install -r requirements.txt
    ENV PORT=10000
    CMD ["python", "main.py"]

## ✔ Testing Steps

1.  Run bot locally.
2.  Open Telegram and send `/start`.
3.  Create profile.
4.  Use second account to test matching.
5.  Verify Accept/Decline flow.

## 📜 License

MIT License.
