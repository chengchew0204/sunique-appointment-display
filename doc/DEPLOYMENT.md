# Deployment Guide

Step-by-step guide for deploying the Appointment Schedule Display to Railway and Netlify.

## Prerequisites

1. GitHub account
2. Railway account (https://railway.app)
3. Netlify account (https://netlify.com)
4. SharePoint credentials (Tenant ID, Client ID, Client Secret)

## Step 1: Push Code to GitHub

1. Initialize git repository if not already done:
```bash
cd /path/to/10-appointment-display
git init
```

2. Add remote repository:
```bash
git remote add origin https://github.com/your-username/appointment-display.git
```

3. Commit and push:
```bash
git add .
git commit -m "Initial appointment display setup"
git push -u origin main
```

## Step 2: Deploy Backend to Railway

### A. Create New Project

1. Go to https://railway.app
2. Click "New Project"
3. Select "Deploy from GitHub repo"
4. Choose your repository
5. Railway will automatically detect Node.js

### B. Configure Environment Variables

In the Railway project dashboard:

1. Go to "Variables" tab
2. Add the following environment variables:

```
SHAREPOINT_TENANT_ID=your-tenant-id
SHAREPOINT_CLIENT_ID=your-client-id
SHAREPOINT_CLIENT_SECRET=your-client-secret
SHAREPOINT_HOSTNAME=suniquecabinetry.sharepoint.com
```

### C. Get Railway URL

1. After deployment completes, go to "Settings" tab
2. Under "Domains", you'll see your Railway URL
3. Copy the URL (e.g., `https://your-app-name.up.railway.app`)

### D. Test Railway Deployment

Visit your Railway URL in browser. You should see:
```json
{
  "status": "ok",
  "message": "Appointment Schedule API Server",
  "endpoints": {
    "health": "GET /",
    "downloadFile": "GET /api/download-schedule"
  }
}
```

## Step 3: Update Frontend Configuration

1. Open `index.html`
2. Find line 569:
```javascript
const API_SERVER_URL = 'http://localhost:3000';
```

3. Replace with your Railway URL:
```javascript
const API_SERVER_URL = 'https://your-app-name.up.railway.app';
```

4. Commit and push the change:
```bash
git add index.html
git commit -m "Update API URL for production"
git push
```

## Step 4: Deploy Frontend to Netlify

### Option A: Drag and Drop

1. Go to https://app.netlify.com
2. Drag and drop your project folder into Netlify
3. Netlify will deploy `index.html` automatically

### Option B: GitHub Integration (Recommended)

1. Go to https://app.netlify.com
2. Click "New site from Git"
3. Choose GitHub and select your repository
4. Configure build settings:
   - **Build command**: (leave empty)
   - **Publish directory**: `.` (root directory)
5. Click "Deploy site"

### Get Netlify URL

After deployment, Netlify will provide a URL like:
```
https://your-site-name.netlify.app
```

You can customize this under Site settings > Domain management.

## Step 5: Test Complete System

1. Open your Netlify URL in a browser
2. You should see:
   - Today's date in the header
   - "Loading appointments..." message
   - Then the appointment table (if there are appointments today)
   - Or "No appointments scheduled for today"

3. Check browser console (F12) for any errors

4. Test the refresh button to ensure data updates

## Step 6: TV Setup

1. Open TV browser and navigate to your Netlify URL
2. Press F11 for full-screen mode
3. Set browser to not sleep/timeout
4. The display will auto-refresh every 5 minutes

## Troubleshooting

### Railway Deployment Issues

**Build fails:**
- Check that `package.json` is in the root directory
- Verify all dependencies are listed
- Check Railway logs for specific errors

**Environment variables not working:**
- Ensure all variables are set correctly (no extra spaces)
- Redeploy after adding variables

### Frontend Issues

**CORS errors:**
- Verify Railway server has CORS enabled
- Check that API_SERVER_URL is correct
- Ensure Railway server is running

**Data not loading:**
- Check browser console for errors
- Verify Railway API endpoint works: visit `https://your-railway-url.app/api/download-schedule`
- Check SharePoint file permissions

### Excel File Issues

**"Could not find Order column":**
- Verify Excel file has proper headers
- Check that file name is "Appoinement.xlsx"
- Ensure file is in SuniqueKnowledgeBase SharePoint site

## Updating the Application

### Update Backend:
1. Make changes to `server.js`
2. Commit and push to GitHub
3. Railway will automatically redeploy

### Update Frontend:
1. Make changes to `index.html`
2. Commit and push to GitHub
3. Netlify will automatically redeploy

## Monitoring

### Railway:
- View logs in Railway dashboard
- Check deployment status
- Monitor resource usage

### Netlify:
- View deployment logs
- Check site status
- Monitor bandwidth usage

## Cost

- **Railway**: Free tier available (500 hours/month)
- **Netlify**: Free tier available (100GB bandwidth/month)

Both should be sufficient for this TV display application.

