# AutoSpares AI
AI-Powered Automobile Spare Parts Management System

<img width="1902" height="937" alt="image" src="https://github.com/user-attachments/assets/3278fb39-6287-4621-a4ea-59c77ed7d706" />
<img width="1918" height="937" alt="image" src="https://github.com/user-attachments/assets/a224c529-1178-43b5-8d30-2dc18fe5a637" />
<img width="1917" height="953" alt="image" src="https://github.com/user-attachments/assets/5e982ac0-2d77-43c1-a14a-5878afeebe98" />


A full-stack web application for managing an automobile spare parts business with three role-locked portals, real AI integration, and automated email notifications.

---

## Portals

| Customer Portal | Company Portal | Data Service |
|---|---|---|
| Browse and order parts | Manage inventory | Manage accounts |
| AI car diagnosis | Process orders | System settings |
| Track orders live | Handle tickets | Login audit logs |
| Book appointments | AI reports | Full audit trail |
| Request out-of-stock parts | Generate invoices | |

---

## Features

- Three role-locked portals — Customer, Company, and Data Service. A company login cannot access the customer portal and vice versa
- Real AI integration — Claude API for car diagnosis, parts chatbot, and inventory analysis with live inventory context injected into every prompt
- Nine-stage order workflow — pending, checking, processing, packing, ready, showroom appointment or courier delivery, delivered
- Automated HTML emails — styled emails for every event including order placed, shipped, delivered, and password reset
- Live inventory editing — update stock and price in the browser without page reload
- Multi-part requests — customers can request multiple out-of-stock parts in one form
- Invoice generation — printable HTML invoices with full item breakdown
- Audit trail — every Data Service admin action logged with reason

---

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python 3.10 / Flask 3.0 |
| Database | SQLite via SQLAlchemy ORM |
| Authentication | Flask-Login with bcrypt password hashing |
| Email | Flask-Mail with Gmail SMTP |
| AI | Anthropic Claude API |
| Templates | Jinja2 |
| Frontend | Vanilla HTML, CSS, JavaScript |

---

## Quick Start

Install dependencies

```bash
pip install -r requirements.txt
```

Run the app

```bash
python app.py
```

Open browser at http://localhost:5000

The database and all tables are created automatically on first run.

---

## First-Time Configuration

All settings are configured inside the app. No terminal commands or config files needed.

**Set your Anthropic API Key**

1. Go to http://localhost:5000
2. Click Sign In as Admin
3. Login with data@autospares.com / data123
4. Click System Settings in the sidebar
5. Paste your API key from console.anthropic.com
6. Click Save API Key

Saved permanently — loads automatically on every restart.

**Set up Gmail for emails (optional)**

On the same Settings page, enter your Gmail address and App Password, then click Save Mail Settings.

---

## Default Login Credentials

| Portal | Email | Password |
|---|---|---|
| Company Staff | admin@autospares.com | admin123 |
| Data Service | data@autospares.com | data123 |
| Customer | Register at /register | — |

> These are demo credentials for local development only. Change them immediately via the Data Service portal before use.

---

## Project Structure

```
autospares/
│
├── app.py
├── requirements.txt
├── README.md
├── .gitignore
│
├── uploads/
│   └── .gitkeep
│
└── templates/
    │
    ├── base.html
    ├── index.html
    ├── login.html
    ├── register.html
    ├── forgot_password.html
    ├── reset_password.html
    │
    ├── customer/
    │   ├── home.html
    │   ├── shop.html
    │   ├── checkout.html
    │   ├── orders.html
    │   ├── track.html
    │   ├── requests.html
    │   ├── new_request.html
    │   ├── request_detail.html
    │   ├── tickets.html
    │   ├── new_ticket.html
    │   ├── ticket_detail.html
    │   ├── diagnose.html
    │   ├── profile.html
    │   └── parts.html
    │
    ├── company/
    │   ├── dashboard.html
    │   ├── orders.html
    │   ├── order_detail.html
    │   ├── inventory.html
    │   ├── add_part.html
    │   ├── requests.html
    │   ├── request_detail.html
    │   ├── tickets.html
    │   ├── ticket_detail.html
    │   ├── customers.html
    │   ├── customer_detail.html
    │   ├── admins.html
    │   ├── chatbot.html
    │   ├── report.html
    │   ├── settings.html
    │   └── mail_settings.html
    │
    └── dataservice/
        ├── dashboard.html
        ├── customer_detail.html
        └── settings.html
```

---

## Database Models

| Model | Purpose |
|---|---|
| User | All accounts — customers, staff, admins |
| Part | Inventory items with stock tracking |
| Order | Customer orders with nine-stage workflow |
| PartRequest | Requests to source out-of-stock parts |
| Ticket | Support tickets with category, priority, and reopen |
| LoginLog | Login history for audit trail |

---

## Order Workflow

```
pending -> checking -> processing -> packing -> received
                                        |
               +------------------------+------------------------+
               |                                                 |
        Showroom Pickup                                 Courier Delivery
               |                                                 |
        appointment_set                               out_for_delivery
               |                                                 |
               +----------------------+--------------------------+
                                      |
                                 delivered
                            (invoice email sent)
```

---

## AI Features

| Feature | Used By | What It Does |
|---|---|---|
| Car Diagnosis | Customer | Describe symptoms, get diagnosis and parts list from live inventory |
| Parts Chatbot | Company Staff | Ask questions, Claude answers with real-time stock context |
| Inventory Report | Company Staff | Health summary, low stock alerts, reorder suggestions |

API key is set once via Data Service > Settings. No environment variables needed.

---

## Email Notifications

| Trigger | Content |
|---|---|
| Customer registers | Welcome message and Customer ID |
| Order placed | Itemised parts table and total |
| Order confirmed | Expected ready date |
| Parts ready | Book appointment or track shipment |
| Order shipped | Courier name and tracking ID |
| Order delivered | Invoice download link |
| Appointment confirmed | Date and time |
| Part request submitted | All parts summary |
| Admin replies to request | Reply and price quote |
| Ticket raised | Category, priority, subject |
| Admin replies to ticket | Reply and updated status |
| Password reset | Secure one-use link |
| New admin created | Login credentials |

Gmail credentials are set via Data Service > Settings. No code changes needed.

---

## Security

- Bcrypt password hashing — never stored plain text
- Portal locking — wrong role is denied with a clear explanation
- Login required on every protected route
- Secure file uploads with extension allowlist
- One-use password reset tokens cleared after use
- Audit log with reason required for every sensitive action

---

## Gmail Setup

1. Enable two-factor authentication on your Gmail account
2. Go to myaccount.google.com, then Security, then App Passwords
3. Generate a password for Mail and copy the 16-character code
4. Log in as Data Service, go to Settings, enter your Gmail and App Password, then save

---
