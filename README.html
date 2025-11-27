<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width,initial-scale=1"/>
  <title>Acoustic Night — Telegram Collaboration Bot — README</title>
  <style>
    :root{
      --bg:#0f1724; --card:#0b1220; --muted:#94a3b8; --accent:#8b5cf6; --glass: rgba(255,255,255,0.03);
      --mono: 'SFMono-Regular', Consolas, "Liberation Mono", Menlo, monospace;
    }
    html,body{height:100%;margin:0;font-family:Inter,Segoe UI,Arial,sans-serif;background:linear-gradient(180deg,#071029 0%, #071833 100%);color:#e6eef8}
    .wrap{max-width:960px;margin:36px auto;padding:28px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border-radius:12px;box-shadow:0 6px 30px rgba(2,6,23,0.7);border:1px solid rgba(255,255,255,0.03)}
    header{display:flex;gap:20px;align-items:center}
    .logo{width:84px;height:84px;border-radius:10px;background:linear-gradient(135deg,var(--accent),#06b6d4);display:flex;align-items:center;justify-content:center;font-weight:700;color:white;font-size:22px;box-shadow:0 6px 20px rgba(139,92,246,0.25)}
    h1{margin:0;font-size:28px}
    p.lead{color:var(--muted);margin:6px 0 20px}
    section{margin-top:20px;padding:18px;border-radius:10px;background:var(--glass);border:1px solid rgba(255,255,255,0.02)}
    h2{margin:0 0 8px;font-size:18px}
    pre{background:#071427;padding:14px;border-radius:8px;overflow:auto;font-family:var(--mono);font-size:13px;color:#cbe7ff}
    code{font-family:var(--mono);font-size:13px;color:#bfe0ff}
    .two{display:grid;grid-template-columns:1fr 1fr;gap:12px}
    ul{color:var(--muted);line-height:1.6}
    .badge{display:inline-block;padding:6px 10px;border-radius:999px;background:rgba(255,255,255,0.03);color:var(--muted);font-size:13px;margin-right:6px}
    footer{margin-top:22px;color:var(--muted);font-size:13px}
    a.link{color:#bfe0ff;text-decoration:none}
    @media (max-width:720px){.two{grid-template-columns:1fr}}
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div class="logo">AN</div>
      <div>
        <h1>Acoustic Night — Telegram Collaboration Bot</h1>
        <p class="lead">A compact Telegram bot letting musicians create profiles, find collaborators (smart matches or browse), and exchange contacts after mutual match.</p>
        <div><span class="badge">Tech: Python</span><span class="badge">DB: PostgreSQL (JSONB)</span><span class="badge">Telegram Bot API</span></div>
      </div>
    </header>

    <section>
      <h2>Source reference</h2>
      <p class="lead">This README was generated from the project source <strong>main.py</strong> and matches the bot logic and DB usage described there. :contentReference[oaicite:1]{index=1}</p>
    </section>

    <section>
      <h2>Quick features</h2>
      <ul>
        <li>Create / edit profile: instruments, who you're seeking, and a short bio (≤120 chars).</li>
        <li>Two browsing modes: <strong>Smart Matches</strong> (mutual interest) and <strong>Browse All</strong>.</li>
        <li>Send collaboration requests; recipient gets <strong>Accept / Decline</strong> UI. Contact (Telegram username) visible only after mutual match.</li>
        <li>Health-check HTTP server (binds to <code>$PORT</code>) — suitable for platforms like Railway/Render.</li>
      </ul>
    </section>

    <section>
      <h2>Installation</h2>
      <div class="two">
        <div>
          <h3>1. Clone & venv</h3>
          <pre><code>git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO
python3 -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows</code></pre>
        </div>
        <div>
          <h3>2. Requirements</h3>
          <pre><code>pip install -r requirements.txt</code></pre>
          <p>Suggested <code>requirements.txt</code>:</p>
          <pre><code>python-telegram-bot==20.6
psycopg2-binary</code></pre>
        </div>
      </div>
    </section>

    <section>
      <h2>Environment variables</h2>
      <p>Set these in your environment or in a <code>.env</code> file:</p>
      <pre><code>TELEGRAM_BOT_TOKEN=123456:ABC-DEF...
DATABASE_URL=postgres://USER:PASSWORD@HOST:5432/DBNAME
PORT=10000   # health-check server port</code></pre>
    </section>

    <section>
      <h2>Database design</h2>
      <p><strong>PostgreSQL</strong> with a single table <code>users</code>. Each row stores user profile JSON in <code>JSONB</code> format.</p>
      <pre><code>CREATE TABLE IF NOT EXISTS users (
  user_id TEXT PRIMARY KEY,
  data JSONB NOT NULL
);</code></pre>
      <p><strong>Example JSON profile</strong>:</p>
      <pre><code>{
  "user_id": "123",
  "name": "John Connor",
  "username": "johnconnor",      # Telegram username (optional)
  "instruments": ["guitarist"],
  "seeking": ["vocalist"],
  "bio": "Looking for vocalist",
  "likes": [],                   # optional in code but present for future features
  "matches": ["456"],
  "pending": ["789"],            # outgoing requests awaiting response
  "viewed": [],
  "created_at": "2025-01-12T10:20:54"
}</code></pre>
      <p class="lead" style="color:var(--muted)">Storing profile as JSONB keeps schema flexible and easy to extend. Indexing strategies (if needed for scale) are discussed below.</p>
    </section>

    <section>
      <h2>Algorithm & core flows</h2>
      <h3>Profile creation</h3>
      <p>On <code>/start</code> the bot gets or creates the profile and updates name/username fields.</p>

      <h3>Editing</h3>
      <p>User picks instruments and seeking categories from a predefined list (INSTRUMENTS). Bio is limited to 120 characters.</p>

      <h3>Browsing / Matching</h3>
      <ol>
        <li><strong>Smart Match</strong>: select candidates where
          <ul>
            <li>candidate.instruments intersects current_user.seeking AND</li>
            <li>current_user.instruments intersects candidate.seeking</li>
          </ul>
        </li>
        <li><strong>Browse All</strong>: show all users except self and those already in <code>pending</code></li>
      </ol>

      <h3>Like → Request → Accept flow</h3>
      <ul>
        <li>User A presses "Let's Collab" on user B → A's profile adds B to <code>pending</code>.</li>
        <li>Bot sends B a message with Accept/Decline buttons (callback_data includes A's user_id).</li>
        <li>If B Accepts: 
          <ul><li>Both users' <code>matches</code> arrays are updated to include each other;</li>
          <li>Bot reveals Telegram username (if available) to the accepting user as contact.</li></ul>
        </li>
        <li>If Declined: pending state removed and request message optionally deleted.</li>
      </ul>

      <h3>Privacy</h3>
      <p>Contact (username) is shown only after mutual match — ensures privacy until both parties agree.</p>
    </section>

    <section>
      <h2>Running locally</h2>
      <pre><code>export TELEGRAM_BOT_TOKEN="..."
export DATABASE_URL="postgres://user:pass@host/db"
export PORT=10000
python main.py</code></pre>
      <p>Open logs to confirm bot started and health-check on <code>http://localhost:10000/</code> returns <code>OK</code>.</p>
    </section>

    <section>
      <h2>Run as systemd service (example)</h2>
      <pre><code>/etc/systemd/system/acousticbot.service

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
WantedBy=multi-user.target</code></pre>
      <p>Commands:</p>
      <pre><code>sudo systemctl daemon-reload
sudo systemctl enable acousticbot
sudo systemctl start acousticbot
sudo journalctl -u acousticbot -f</code></pre>
    </section>

    <section>
      <h2>Docker & docker-compose (optional)</h2>
      <h3>Dockerfile</h3>
      <pre><code>FROM python:3.11-slim
WORKDIR /app
COPY . /app
RUN python -m pip install --upgrade pip \
  && pip install -r requirements.txt
ENV PORT=10000
CMD ["python", "main.py"]</code></pre>

      <h3>docker-compose.yml (example)</h3>
      <pre><code>version: "3.8"
services:
  db:
    image: postgres:15
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: acoustic
    volumes:
      - db_data:/var/lib/postgresql/data
  bot:
    build: .
    environment:
      TELEGRAM_BOT_TOKEN: ${TELEGRAM_BOT_TOKEN}
      DATABASE_URL: postgres://postgres:postgres@db:5432/acoustic
      PORT: 10000
    depends_on:
      - db
volumes:
  db_data:</code></pre>
    </section>

    <section>
      <h2>Scaling & Improvements (notes)</h2>
      <ul>
        <li><strong>Indexes:</strong> if users grow to 10k+, add a materialized view or inverted index using <code>jsonb_path_ops</code> / GIN indexes for common queries on instruments/seeking.</li>
        <li><strong>Pagination:</strong> current in-memory browsing uses arrays — switch to DB-side pagination for scale.</li>
        <li><strong>Notifications:</strong> consider job queue (Redis/RQ or Celery) for sending messages and heavy tasks.</li>
        <li><strong>Private message UX:</strong> add richer profile cards and photos if you want multimedia profiles.</li>
        <li><strong>Rate-limits & safety:</strong> implement basic rate-limiting for message sends and validate usernames/IDs to avoid spam.</li>
      </ul>
    </section>

    <section>
      <h2>Testing</h2>
      <ol>
        <li>Start DB & run bot locally.</li>
        <li>From Telegram account A: /start, set profile.</li>
        <li>From Telegram account B: /start, set complementary profile.</li>
        <li>From A: Browse → Like B → B should receive Accept/Decline.</li>
        <li>Accept → both profiles must include each other's IDs in <code>matches</code> and username visible.</li>
      </ol>
    </section>

    <section>
      <h2>Contributing & TODOs</h2>
      <ul>
        <li>Add user photos and audio samples to profile.</li>
        <li>Switch DB to normalized tables if complex querying is required (users, instruments, user_instruments, requests).</li>
        <li>Unit tests for DB wrappers and matching algorithm.</li>
        <li>Better UX for long lists (carousel, inline media).</li>
      </ul>
    </section>

    <footer>
      <p>Made for your repo — drop more code or say "make a Docker image & GitHub Actions CI" and I'll add those files.  
      (Reference implementation: <strong>main.py</strong>). :contentReference[oaicite:2]{index=2}</p>
    </footer>
  </div>
</body>
</html>
