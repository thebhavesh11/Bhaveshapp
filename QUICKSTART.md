# 🚀 SmartFlow AI - Quick Start Guide

Get up and running in 5 minutes!

## Prerequisites

- Node.js 18+ installed
- PostgreSQL database
- OpenAI API key

## Step 1: Clone & Install (2 min)

```bash
git clone <your-repo-url>
cd smartflow-ai

# Install all dependencies
npm install
cd backend && npm install
cd ../frontend && npm install
cd ..
```

## Step 2: Configure Environment (1 min)

```bash
# Copy environment template
cp .env.example .env

# Edit .env with your details
nano .env
```

Minimum required variables:
```env
DATABASE_URL="postgresql://user:pass@localhost:5432/smartflow"
OPENAI_API_KEY="sk-..."
```

## Step 3: Setup Database (1 min)

```bash
cd backend

# Run migrations
npx prisma migrate deploy

# Generate Prisma client
npx prisma generate
```

## Step 4: Start Application (1 min)

Open two terminals:

**Terminal 1 - Backend:**
```bash
cd backend
npm start
```

**Terminal 2 - Frontend:**
```bash
cd frontend
npm run dev
```

## Step 5: Connect WhatsApp (< 1 min)

1. Open http://localhost:3001
2. Navigate to "WhatsApp" page
3. Scan QR code with your phone
4. ✅ Done! Start receiving messages

## 🎉 You're Ready!

Send a message to your connected WhatsApp number and watch the AI reply automatically!

## Next Steps

- Configure AI settings in the dashboard
- Customize the system prompt
- View leads and conversations
- Check analytics

## Need Help?

- See full README.md for detailed documentation
- Check troubleshooting section
- Review logs in console

---

**Enjoy automating your WhatsApp! 🤖**
