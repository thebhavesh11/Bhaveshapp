# SmartFlow AI Automation Platform

> **Production-Ready WhatsApp AI Automation Platform** - Automatically handle WhatsApp messages, qualify leads, and engage customers using AI.

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![Node](https://img.shields.io/badge/node-18+-green.svg)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

## 🚀 Features

- ✅ **WhatsApp Integration** - Connect your WhatsApp account with QR code
- 🤖 **AI-Powered Responses** - Automatic replies using OpenAI, Gemini, or OpenRouter
- 📊 **Lead Management** - Automatic lead creation and qualification
- 🎯 **Smart Lead Scoring** - AI-driven scoring (Hot, Warm, Cold, Spam)
- 💬 **Conversation Tracking** - Full message history and analytics
- 📈 **Dashboard & Metrics** - Real-time insights and statistics
- 🔄 **Session Persistence** - WhatsApp connection survives server restarts
- 🎨 **Modern UI** - Clean Next.js dashboard with real-time updates

## 📋 Tech Stack

### Backend
- Node.js & Express.js
- WhatsApp Web.js (WhatsApp integration)
- Prisma (ORM)
- PostgreSQL (Database)
- OpenAI, Gemini, OpenRouter (AI providers)

### Frontend
- Next.js 14 (App Router)
- React
- Tailwind CSS
- Recharts (Data visualization)
- Axios (API client)

### Deployment
- Railway (Recommended)
- Docker support
- PostgreSQL database

## 🏗️ Project Structure

```
smartflow-ai/
├── backend/
│   ├── src/
│   │   ├── controllers/      # API controllers
│   │   ├── routes/           # Express routes
│   │   ├── services/         # Business logic
│   │   │   ├── ai/          # AI integration
│   │   │   ├── whatsapp/    # WhatsApp service
│   │   │   └── database/    # Prisma client
│   │   ├── middleware/       # Express middleware
│   │   ├── utils/           # Utilities
│   │   └── server.js        # Main server file
│   ├── prisma/
│   │   └── schema.prisma    # Database schema
│   └── package.json
├── frontend/
│   ├── app/                 # Next.js pages (App Router)
│   ├── components/          # React components
│   └── package.json
├── .env.example
├── Dockerfile
├── railway.json
└── README.md
```

## 🔧 Installation

### Prerequisites

- Node.js 18+ and npm 9+
- PostgreSQL database
- OpenAI API key (or Gemini/OpenRouter)

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/smartflow-ai.git
cd smartflow-ai
```

### 2. Install Dependencies

```bash
# Install root dependencies
npm install

# Install backend dependencies
cd backend
npm install

# Install frontend dependencies
cd ../frontend
npm install
cd ..
```

### 3. Configure Environment Variables

Create a `.env` file in the root directory:

```bash
cp .env.example .env
```

Edit `.env` with your credentials:

```env
# Database
DATABASE_URL="postgresql://user:password@localhost:5432/smartflow_ai"

# Server
PORT=3000
NODE_ENV=production
FRONTEND_URL=http://localhost:3001

# AI Provider (choose one or more)
OPENAI_API_KEY=your_openai_api_key_here
GEMINI_API_KEY=your_gemini_api_key_here
OPENROUTER_API_KEY=your_openrouter_api_key_here

# Default AI Settings
DEFAULT_AI_PROVIDER=openai
DEFAULT_AI_MODEL=gpt-3.5-turbo
DEFAULT_AI_TEMPERATURE=0.7
```

### 4. Set Up Database

```bash
cd backend

# Run Prisma migrations
npx prisma migrate dev

# Generate Prisma Client
npx prisma generate
```

### 5. Start the Application

**Development Mode:**

```bash
# Terminal 1 - Backend
cd backend
npm run dev

# Terminal 2 - Frontend
cd frontend
npm run dev
```

**Production Mode:**

```bash
# Terminal 1 - Backend
cd backend
npm start

# Terminal 2 - Frontend
cd frontend
npm run build
npm start
```

Access the application:
- Frontend: http://localhost:3001
- Backend API: http://localhost:3000

## 📱 WhatsApp Connection

### Connecting WhatsApp

1. Navigate to the **WhatsApp** page in the dashboard
2. A QR code will be automatically generated
3. Open WhatsApp on your phone
4. Go to **Settings** → **Linked Devices** → **Link a Device**
5. Scan the QR code displayed on your screen
6. Wait for connection confirmation

### Session Persistence

- WhatsApp sessions are stored in `backend/whatsapp-session/`
- Sessions persist across server restarts
- Auto-reconnection on disconnect
- QR code regenerates if session expires

## 🤖 How It Works

### Automation Pipeline

```
Incoming WhatsApp Message
         ↓
Check if phone number exists
         ↓
Create lead if new
         ↓
Store message in database
         ↓
Send to AI for response generation
         ↓
Send AI reply to WhatsApp
         ↓
Store AI message
         ↓
Run lead scoring AI
         ↓
Update dashboard metrics
```

### Lead Scoring

The AI analyzes conversations and assigns scores:

- **🔥 HOT** - Strong buying intent, ready to purchase
- **🌡️ WARM** - Interested and engaged
- **❄️ COLD** - Minimal engagement
- **🚫 SPAM** - Irrelevant or spam messages

## 🚢 Railway Deployment

### 1. Prepare for Deployment

Ensure your code is pushed to GitHub:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/yourusername/smartflow-ai.git
git push -u origin main
```

### 2. Deploy to Railway

1. Go to [Railway.app](https://railway.app)
2. Click **"New Project"** → **"Deploy from GitHub repo"**
3. Select your `smartflow-ai` repository
4. Railway will detect the Dockerfile automatically

### 3. Add PostgreSQL Database

1. In your Railway project, click **"New"** → **"Database"** → **"PostgreSQL"**
2. Railway will create a database and provide a `DATABASE_URL`

### 4. Configure Environment Variables

In Railway project settings, add these variables:

```
DATABASE_URL=<automatically_set_by_railway>
NODE_ENV=production
PORT=3000
FRONTEND_URL=https://your-app.railway.app
OPENAI_API_KEY=your_key_here
DEFAULT_AI_PROVIDER=openai
DEFAULT_AI_MODEL=gpt-3.5-turbo
DEFAULT_AI_TEMPERATURE=0.7
```

### 5. Deploy

Railway will automatically:
- Build the Docker image
- Run database migrations
- Start the application
- Provide a public URL

### 6. Connect WhatsApp

1. Visit your Railway app URL
2. Navigate to WhatsApp page
3. Scan QR code with your phone

## 📊 API Endpoints

### WhatsApp
- `GET /api/whatsapp/status` - Connection status
- `GET /api/whatsapp/qr` - Get QR code
- `GET /api/whatsapp/session` - Session info

### Leads
- `GET /api/leads` - List all leads
- `GET /api/leads/:id` - Get lead details
- `PUT /api/leads/:id` - Update lead
- `GET /api/leads/stats` - Lead statistics

### Conversations
- `GET /api/conversations` - List conversations
- `GET /api/conversations/:id` - Get conversation with messages
- `PUT /api/conversations/:id` - Update conversation

### Messages
- `POST /api/messages/send` - Send manual message
- `GET /api/messages/:conversationId` - Get messages

### Dashboard
- `GET /api/dashboard/metrics` - Dashboard metrics
- `GET /api/dashboard/analytics` - Conversation analytics

### AI Settings
- `GET /api/ai-settings` - Get AI configuration
- `PUT /api/ai-settings/:id` - Update AI settings
- `POST /api/ai-settings/test` - Test AI configuration

## 🎨 Frontend Pages

- **Dashboard** - Overview with metrics and activity
- **Leads** - Manage and filter leads
- **Conversations** - View message history
- **WhatsApp** - Connection and QR code
- **AI Settings** - Configure AI behavior
- **Settings** - Business and system settings

## 🔐 Environment Variables Reference

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| `DATABASE_URL` | PostgreSQL connection string | Yes | - |
| `PORT` | Backend server port | No | 3000 |
| `NODE_ENV` | Environment (development/production) | No | production |
| `FRONTEND_URL` | Frontend URL for CORS | No | http://localhost:3001 |
| `OPENAI_API_KEY` | OpenAI API key | If using OpenAI | - |
| `GEMINI_API_KEY` | Google Gemini API key | If using Gemini | - |
| `OPENROUTER_API_KEY` | OpenRouter API key | If using OpenRouter | - |
| `DEFAULT_AI_PROVIDER` | AI provider (openai/gemini/openrouter) | No | openai |
| `DEFAULT_AI_MODEL` | AI model name | No | gpt-3.5-turbo |
| `DEFAULT_AI_TEMPERATURE` | AI temperature (0-2) | No | 0.7 |
| `DEFAULT_AI_MAX_TOKENS` | Max response tokens | No | 500 |

## 🛠️ Development

### Database Management

```bash
# Create new migration
npx prisma migrate dev --name migration_name

# Reset database
npx prisma migrate reset

# Open Prisma Studio
npx prisma studio
```

### Logs

Logs are output to console and optionally to file:

```env
LOG_LEVEL=info
LOG_FILE_PATH=./logs/app.log
```

## 📝 Notes

### WhatsApp Limitations

- One WhatsApp account per instance
- Max 4 linked devices per WhatsApp account
- Group messages are ignored by default
- Media messages (images, audio) are received but not processed

### AI Provider Recommendations

- **OpenAI** - Best overall quality, reliable
- **Gemini** - Cost-effective, good for high volume
- **OpenRouter** - Access to multiple models

### Scaling

- Use PostgreSQL connection pooling for high traffic
- Consider Redis for session caching
- Deploy multiple instances with load balancer
- Use dedicated WhatsApp Business API for production scale

## 🐛 Troubleshooting

### WhatsApp Won't Connect

1. Check if Chromium is installed (required for puppeteer)
2. Verify session directory has write permissions
3. Try deleting `whatsapp-session` folder and reconnecting
4. Check server logs for errors

### Database Connection Issues

1. Verify `DATABASE_URL` is correct
2. Ensure PostgreSQL is running
3. Check firewall settings
4. Run `npx prisma migrate deploy`

### AI Not Responding

1. Verify API key is set correctly
2. Check AI provider status
3. Test configuration in AI Settings page
4. Review server logs for API errors

## 📄 License

MIT License - See LICENSE file for details

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📧 Support

For issues and questions:
- Create an issue on GitHub
- Check existing documentation
- Review server logs

---

**Built with ❤️ using Node.js, Next.js, and AI**
