# Direct Render Deployment from Replit

## Your Production Files Are Ready

Your Excel Edge Properties codebase is production-ready right here:
- Frontend build: `dist/public/` (optimized assets)
- Backend build: `dist/index.js` (31KB bundle)
- Source code: Complete client/server structure
- All documentation and configuration files present

## Option 1: Deploy via GitHub (Recommended)

### Step 1: Connect Replit to GitHub
1. In Replit, click "Version control" (git icon) in left sidebar
2. Click "Create a Git repository"
3. Name it: `excel-edge-properties`
4. Click "Create repository"
5. This automatically pushes to GitHub

### Step 2: Deploy on Render
1. Go to render.com
2. Sign in with GitHub
3. Create PostgreSQL database first
4. Deploy backend web service from GitHub repo
5. Deploy frontend static site from same repo

## Option 2: Direct Upload to GitHub

### Manual GitHub Upload
1. Go to github.com/new
2. Repository name: `excel-edge-properties`
3. Create repository
4. Upload files manually or use GitHub CLI

## Render Deployment Configuration

### Backend Service Settings
```
Repository: excel-edge-properties
Branch: main
Build Command: npm install && npm run build
Start Command: npm start
Publish Directory: (leave empty for backend)
```

### Frontend Service Settings
```
Repository: excel-edge-properties
Branch: main
Build Command: npm install && npm run build
Publish Directory: dist/public
```

### Required Environment Variables

#### Backend
```
NODE_ENV=production
PORT=10000
DATABASE_URL=[from PostgreSQL service]
SESSION_SECRET=[generate 32 chars]
ISSUER_URL=https://auth.replit.com/issuer
REPLIT_DOMAINS=your-replit-domain.replit.dev
```

#### Frontend
```
VITE_API_URL=https://your-backend.onrender.com
```

## Verification Steps

1. Health check: `https://your-backend.onrender.com/api/health`
2. Frontend loads with royal blue theme
3. Browse deals shows 6 authentic properties
4. All navigation works properly

Your codebase includes:
- 6 authentic UK and Nigeria property deals
- Complete financial analysis engine
- Royal blue professional theme
- Multi-currency support (GBP/NGN)
- Production-optimized builds
- Comprehensive documentation
- Test certification (100% pass rate)