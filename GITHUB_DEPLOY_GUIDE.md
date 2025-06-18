# Step-by-Step GitHub & Render Deployment Guide

## Part 1: Push to GitHub

### Step 1: Create GitHub Repository
1. Go to https://github.com
2. Click "New repository" (green button)
3. Repository name: `excel-edge-properties`
4. Description: `Property investment platform connecting sourcers with investors`
5. Set to Public or Private (your choice)
6. DO NOT initialize with README, .gitignore, or license (we already have these)
7. Click "Create repository"

### Step 2: Add GitHub Remote
In your terminal/command line:
```bash
git remote add origin https://github.com/YOUR_USERNAME/excel-edge-properties.git
```
Replace `YOUR_USERNAME` with your actual GitHub username.

### Step 3: Stage and Commit Files
```bash
git add .
git commit -m "Initial commit: Excel Edge Properties production-ready app"
```

### Step 4: Push to GitHub
```bash
git push -u origin main
```

If you get an error about the default branch, try:
```bash
git branch -M main
git push -u origin main
```

## Part 2: Deploy on Render.com

### Step 1: Create Render Account
1. Go to https://render.com
2. Sign up with GitHub account (recommended)
3. Authorize Render to access your repositories

### Step 2: Create PostgreSQL Database
1. In Render dashboard, click "New +"
2. Select "PostgreSQL"
3. Settings:
   - Name: `excel-edge-properties-db`
   - Database: `excel_edge_properties`
   - User: `excel_edge_user`
   - Region: Choose closest to your location
   - Plan: Free
4. Click "Create Database"
5. **IMPORTANT**: Copy the "External Database URL" - you'll need this

### Step 3: Deploy Backend API
1. Click "New +" → "Web Service"
2. Connect your GitHub repository: `excel-edge-properties`
3. Settings:
   - Name: `excel-edge-properties-api`
   - Branch: `main`
   - Runtime: `Node`
   - Build Command: `npm install && npm run build`
   - Start Command: `npm start`
   - Plan: Free

4. Environment Variables (click "Add Environment Variable"):
   ```
   NODE_ENV = production
   PORT = 10000
   DATABASE_URL = [paste the External Database URL from Step 2]
   SESSION_SECRET = [generate 32 random characters - use https://www.allkeysgenerator.com/Random/Security-Encryption-Key-Generator.aspx]
   ISSUER_URL = https://auth.replit.com/issuer
   REPLIT_DOMAINS = your-domain.replit.dev
   ```

5. Advanced Settings:
   - Health Check Path: `/api/health`
   
6. Click "Create Web Service"

### Step 4: Deploy Frontend
1. Click "New +" → "Static Site"
2. Connect same GitHub repository: `excel-edge-properties`
3. Settings:
   - Name: `excel-edge-properties-frontend`
   - Branch: `main`
   - Build Command: `npm install && npm run build`
   - Publish Directory: `dist/public`

4. Environment Variables:
   ```
   VITE_API_URL = https://excel-edge-properties-api.onrender.com
   ```
   (Use the exact URL from your backend service)

5. Click "Create Static Site"

## Part 3: Verification Steps

### Step 1: Check Database
1. Go to your PostgreSQL service
2. Verify status shows "Available"
3. Note the connection details

### Step 2: Check Backend API
1. Go to your web service
2. Wait for build to complete (5-10 minutes)
3. Check logs for any errors
4. Test health endpoint: `https://your-api-url.onrender.com/api/health`
5. Should return: `{"status":"healthy","timestamp":"...","service":"excel-edge-properties-api"}`

### Step 3: Check Frontend
1. Go to your static site
2. Wait for build to complete
3. Click the generated URL
4. Verify the app loads with royal blue theme
5. Test navigation between pages

### Step 4: Test Full Functionality
1. Visit frontend URL
2. Click "Browse Deals" - should show 6 property deals
3. Try filtering by strategy
4. Attempt login (will redirect to Replit Auth)
5. Check all navigation links work

## Part 4: Configure Custom Domains (Optional)

### Backend Domain
1. In backend service settings
2. Custom Domains → Add Custom Domain
3. Enter: `api.yourdomain.com`
4. Configure DNS CNAME: `api.yourdomain.com` → `excel-edge-properties-api.onrender.com`

### Frontend Domain
1. In frontend service settings
2. Custom Domains → Add Custom Domain
3. Enter: `yourdomain.com`
4. Configure DNS A record or CNAME as instructed

## Part 5: Enable Auto-Deploy

### Both Services
1. Go to service settings
2. Build & Deploy → Auto-Deploy
3. Enable "Auto-Deploy: Yes"
4. Now every push to main branch triggers deployment

## Troubleshooting Common Issues

### Build Failures
- Check build logs in Render dashboard
- Verify Node.js version compatibility
- Ensure all dependencies are in package.json

### Database Connection Errors
- Verify DATABASE_URL is correctly set
- Check PostgreSQL service status
- Ensure database name matches schema

### CORS Errors
- Verify VITE_API_URL matches backend URL exactly
- Check backend CORS configuration
- Ensure no trailing slashes in URLs

### Frontend Not Loading
- Check static site build logs
- Verify publish directory is `dist/public`
- Ensure build command completes successfully

## Final Checklist

✅ Repository pushed to GitHub
✅ PostgreSQL database created and running
✅ Backend API deployed and health check responds
✅ Frontend deployed and loads correctly
✅ Environment variables configured
✅ Auto-deploy enabled
✅ All functionality tested

## Live URLs
- Frontend: `https://excel-edge-properties-frontend.onrender.com`
- Backend API: `https://excel-edge-properties-api.onrender.com`
- Health Check: `https://excel-edge-properties-api.onrender.com/api/health`