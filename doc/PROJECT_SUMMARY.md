# Project Summary: Appointment Schedule Display

## Overview

TV display system for showing today's scheduled pick-up appointments from SharePoint Excel file.

## Project Structure

```
10-appointment-display/
├── server.js              # Node.js proxy server for SharePoint API
├── index.html            # Frontend TV display interface
├── package.json          # Node.js dependencies
├── .gitignore           # Git ignore rules
├── env.template         # Environment variables template
├── README.md            # Main documentation
├── doc/
│   ├── DEPLOYMENT.md    # Deployment guide for Railway & Netlify
│   ├── TESTING.md       # Local testing instructions
│   └── PROJECT_SUMMARY.md # This file
└── img/
    └── logo.png         # Sunique logo
```

## Key Features

### Backend (server.js)
- Express.js server
- SharePoint authentication via Microsoft Graph API
- Downloads Appoinement.xlsx from SharePoint
- CORS enabled for browser access
- Deployed on Railway

### Frontend (index.html)
- TV-optimized display (72px font size)
- Auto-refresh every 5 minutes
- Manual refresh button
- Displays Order Number & Appointment Time
- Filters appointments for today only
- Deployed on Netlify

## Technology Stack

### Backend
- Node.js
- Express.js
- node-fetch
- CORS middleware
- dotenv

### Frontend
- Vanilla JavaScript
- XLSX.js for Excel parsing
- CSS3 with responsive design
- No frameworks required

## Data Flow

```
SharePoint Excel File (Appoinement.xlsx)
    ↓
Microsoft Graph API
    ↓
Railway Server (server.js)
    ↓ (CORS-enabled API)
Frontend Browser (index.html)
    ↓
TV Display
```

## Excel File Requirements

The system expects an Excel file with:
- **Order column**: Contains order numbers
- **Appointment Time column**: Shows scheduled pick-up times
- **Date column**: Used to filter for today's appointments

The parser automatically detects these columns by searching header row for keywords.

## Deployment Architecture

### Production
- **Backend**: Railway (https://railway.app)
- **Frontend**: Netlify (https://netlify.com)
- **Data Source**: SharePoint SuniqueKnowledgeBase site

### Local Development
- **Backend**: http://localhost:3000
- **Frontend**: Open index.html in browser
- **Data Source**: Same SharePoint file

## Environment Variables

Required for backend server:
```
SHAREPOINT_TENANT_ID     - Azure AD tenant ID
SHAREPOINT_CLIENT_ID     - App registration client ID
SHAREPOINT_CLIENT_SECRET - App registration secret
SHAREPOINT_HOSTNAME      - SharePoint hostname
PORT                     - Server port (optional, default 3000)
```

## API Endpoints

### GET /
Health check endpoint
Returns server status and available endpoints

### GET /api/download-schedule
Downloads the appointment Excel file from SharePoint
Returns binary Excel data

## Frontend Configuration

Key configuration in index.html:
```javascript
const API_SERVER_URL = 'http://localhost:3000'; // Update for production
```

Auto-refresh interval:
```javascript
300000 // 5 minutes in milliseconds
```

## Visual Design

### Colors
- Background: Olive green gradient (#3d4528 → #515a36)
- Text: White (#ffffff)
- Row background: Yellow (#fffc54)
- Row hover: Scaled and shadowed

### Typography
- Font: -apple-system, BlinkMacSystemFont, "Segoe UI"
- Table data: 72px bold
- Headers: 48px
- Footer stats: 32px

### Layout
- Header with logo and refresh controls
- Full-width table with 2 columns (50% each)
- Fixed footer with appointment count
- Responsive for different TV resolutions

## Browser Compatibility

Tested and optimized for:
- Chrome (recommended)
- Firefox
- Safari
- Edge

## Screen Resolutions

Optimized for:
- 3840x2160 (4K)
- 1920x1080 (Full HD)
- 1366x768 (HD)

## Security Considerations

- SharePoint credentials stored only on Railway (environment variables)
- Frontend has no embedded credentials
- CORS restricted to browser access
- .env file excluded from git repository

## Maintenance

### Update Backend
1. Modify server.js
2. Push to GitHub
3. Railway auto-deploys

### Update Frontend
1. Modify index.html
2. Push to GitHub
3. Netlify auto-deploys

### Update Excel File
No code changes needed - system automatically fetches latest file

## Future Enhancements (Optional)

- Status indicators for completed appointments
- Multiple location support
- Customer name display
- Weekly view option
- Mobile responsive design
- Dark/light theme toggle
- Email notifications
- Integration with other systems

## Support & Troubleshooting

See documentation:
- README.md - Overview and quick start
- doc/DEPLOYMENT.md - Deployment instructions
- doc/TESTING.md - Testing guide

