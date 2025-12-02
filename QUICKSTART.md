# Quick Start Guide

Get the Appointment Schedule Display running in 5 minutes.

## Local Testing (5 steps)

### 1. Install Dependencies
```bash
npm install
```

### 2. Configure Environment
```bash
# Copy the template
cp env.template .env

# Edit .env with your SharePoint credentials
# SHAREPOINT_TENANT_ID=...
# SHAREPOINT_CLIENT_ID=...
# SHAREPOINT_CLIENT_SECRET=...
# SHAREPOINT_HOSTNAME=suniquecabinetry.sharepoint.com
```

### 3. Start Server
```bash
npm start
```

### 4. Test API
Open browser: http://localhost:3000

Should see: `{"status": "ok", "message": "Appointment Schedule API Server"}`

### 5. Open Display
Open `index.html` in your browser

Should see today's appointments (or "No appointments scheduled for today")

## Production Deployment (3 steps)

### 1. Deploy Backend to Railway
```bash
# Push to GitHub first
git add .
git commit -m "Initial setup"
git push

# Then on Railway:
# - Connect GitHub repo
# - Add environment variables
# - Auto-deploys
```

### 2. Update Frontend
```javascript
// In index.html, line 569:
const API_SERVER_URL = 'https://your-app-name.up.railway.app';
```

### 3. Deploy Frontend to Netlify
- Connect GitHub repo to Netlify
- Auto-deploys from main branch

## Verify Everything Works

- [ ] Railway API health check returns OK
- [ ] Frontend loads without errors
- [ ] Appointments display correctly
- [ ] Refresh button works
- [ ] TV display looks good in full-screen

## Next Steps

- Set up TV browser to open Netlify URL
- Enable full-screen mode (F11)
- Configure browser to not sleep
- System auto-refreshes every 5 minutes

## Need Help?

- See `README.md` for full documentation
- See `doc/TESTING.md` for testing guide
- See `doc/DEPLOYMENT.md` for detailed deployment steps

