# Nazarbayev University Acoustic Night club  — Telegram Artists Collaboration Bot

A Telegram bot that helps musicians create profiles, find collaborators, and connect after a mutual match.

## Features

- **Create & Edit Profile**
  - Choose instruments you play from 10+ options
  - Specify instruments you're seeking
  - Write a short bio (max 120 characters)
- **Smart Matching System**
  - 🎯 **Smart Matches**: Find users based on mutual instrument interests
  - 🔀 **Browse All**: Discover all musicians in swipe-style interface
- **Secure Collaboration**
  - Send "Let's Collab" requests to other musicians
  - Contact information revealed **only after mutual match**
  - Real-time notification system for requests

## Tech Stack

- **Python 3.10+**
- **python-telegram-bot v20.6**
- **PostgreSQL with JSONB**
- **psycopg2**

## Quick Start

```bash
git clone https://github.com/CheffCorleOne/NU_acousticnigtbot.git
cd NU_acousticnigtbot
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```
## Configuration
Set environment variables:
```.env
TELEGRAM_BOT_TOKEN=your_bot_token
DATABASE_URL=postgresql://user:pass@host/db
```

## Database
Simple JSONB schema:
```sql;
CREATE TABLE IF NOT EXISTS users (
    user_id TEXT PRIMARY KEY,
    data JSONB NOT NULL
);
```
## Running
```bash
python main.py
```

