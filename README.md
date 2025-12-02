# Sunique Appointment Schedule - TV Display

A TV display system showing today's appointment schedule for pick-up orders. Features large, color-coded displays optimized for viewing from a distance, with Sunique branding.

## System Components

- **Node.js Proxy Server** (Railway): Handles SharePoint authentication and file downloads
- **HTML Display Interface**: Large-format TV interface with real-time appointment updates

## Architecture

```
TV Display (Browser) → Node.js Server (Railway) → SharePoint/Microsoft Graph API
```

The proxy server avoids CORS issues and keeps credentials secure.

## Features

**TV-Optimized Display**
- Large, easy-to-read fonts (72px) for TV viewing
- Clean two-column layout: Order Number & Appointment Time
- Sunique brand colors and logo integration
- Auto-refresh every 5 minutes

**Real-Time Updates**
- Automatically displays only today's appointments
- Shows order numbers and scheduled pick-up times
- Manual refresh button available
- Last updated timestamp

**TV-Ready Design**
- Optimized for 1920x1080, 1366x768, and other common TV resolutions
- High contrast design with gradient backgrounds
- Responsive layout for different screen sizes

## Excel File Structure

**File Name:** Appoinement.xlsx  
**Location:** SharePoint SuniqueKnowledgeBase site

The system automatically detects:
- **Order column** - Contains order numbers to display
- **Appointment Time column** - Shows scheduled pick-up times
- **Date column** - Used to filter appointments for today

The parser will automatically find these columns by searching for keywords in the header row.

## Deployment Instructions

### 1. Deploy Server to Railway

1. Create a Railway account at https://railway.app
2. Click "New Project" → "Deploy from GitHub repo"
3. Select this repository
4. Railway will auto-detect Node.js and use `npm start`

### 2. Configure Environment Variables on Railway

In your Railway project dashboard, add these environment variables:

```
SHAREPOINT_TENANT_ID=your-tenant-id
SHAREPOINT_CLIENT_ID=your-client-id
SHAREPOINT_CLIENT_SECRET=your-client-secret
SHAREPOINT_HOSTNAME=your-hostname.sharepoint.com
```

Create a `.env` file locally (see `.env.example`) but do not commit this file to git!

### 3. Get Your Railway URL

After deployment, Railway will provide a URL like:
```
https://your-app-name.up.railway.app
```

### 4. Deploy HTML to Netlify

1. Create a Netlify account at https://netlify.com
2. Drag and drop the `index.html` and `img/` folder to Netlify
3. Or connect to GitHub for automatic deployments

### 5. Update HTML Configuration

Open `index.html` and update line 569:

```javascript
const API_SERVER_URL = 'https://your-app-name.up.railway.app';
```

Replace with your actual Railway URL.

## Local Development

To test locally before deploying:

1. Install dependencies:
```bash
npm install
```

2. Create a `.env` file with your SharePoint credentials:
```
SHAREPOINT_TENANT_ID=your-tenant-id
SHAREPOINT_CLIENT_ID=your-client-id
SHAREPOINT_CLIENT_SECRET=your-client-secret
SHAREPOINT_HOSTNAME=suniquecabinetry.sharepoint.com
```

3. Start the server:
```bash
npm start
```

4. Open `index.html` in your browser
   - Make sure `API_SERVER_URL` is set to `http://localhost:3000`
   - The page will automatically load today's appointments

## API Endpoints

- `GET /` - Health check and API information
- `GET /api/download-schedule` - Download the appointment schedule Excel file

## Security Notes

- Credentials are stored as environment variables on Railway (secure)
- The HTML file contains no credentials (safe to deploy to Netlify)
- CORS is enabled to allow browser access
- Never commit the `.env` file to version control

## Files

- `server.js` - Express server with SharePoint proxy
- `package.json` - Node.js dependencies
- `index.html` - Client interface for TV display
- `.env` - Local environment variables (not in git)
- `.env.example` - Template for environment variables
- `img/logo.png` - Sunique logo

## Using the TV Display

1. **Open on TV Browser**: Navigate to the deployed Netlify URL
2. **Full Screen Mode**: Press F11 for full-screen display
3. **Auto-Refresh**: The page auto-refreshes every 5 minutes
4. **Manual Refresh**: Click the refresh button in the header

## Troubleshooting

**Error: "NetworkError when attempting to fetch resource"**
- Make sure the Railway server is running
- Check that API_SERVER_URL in HTML matches your Railway URL
- Verify environment variables are set correctly on Railway

**Error: "Authentication failed"**
- Verify SharePoint credentials in Railway environment variables
- Check that the client secret hasn't expired

**"No appointments scheduled for today"**
- This is normal if there are no appointments for today's date
- The system filters by exact date match

**"Could not find Order column in Excel file"**
- Verify the Excel file has a column header containing "Order"
- Check that the file structure matches the expected format

## Design Specifications

- **Background**: Sunique olive green gradient (#3d4528 → #515a36)
- **Logo**: Sunique logo (60px height)
- **Primary Font Size**: 72px (table data)
- **Header Font Size**: 48px
- **Responsive**: Scales for 4K (3840x2160), Full HD (1920x1080), and HD (1366x768)
- **Auto-Refresh Interval**: 5 minutes (300000ms)

## GitHub & Deployment Workflow

1. **Push to GitHub**:
```bash
git add .
git commit -m "Initial appointment display setup"
git push origin main
```

2. **Railway Deployment**:
   - Connect Railway to your GitHub repository
   - Railway will auto-deploy on every push to main
   - Set environment variables in Railway dashboard

3. **Netlify Deployment**:
   - Connect Netlify to your GitHub repository
   - Netlify will auto-deploy the HTML on every push
   - Or manually drag-drop `index.html` and `img/` folder
