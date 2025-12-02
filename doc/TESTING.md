# Local Testing Guide

Guide for testing the appointment display locally before deployment.

## Setup for Local Testing

### 1. Install Dependencies

```bash
cd /Users/zackwu204/CursorAI/Sunique/10-appointment-display
npm install
```

### 2. Configure Environment Variables

Create a `.env` file in the project root:

```bash
# Copy from your existing credentials
SHAREPOINT_TENANT_ID=your-tenant-id
SHAREPOINT_CLIENT_ID=your-client-id
SHAREPOINT_CLIENT_SECRET=your-client-secret
SHAREPOINT_HOSTNAME=suniquecabinetry.sharepoint.com
PORT=3000
```

### 3. Verify API Configuration

Open `index.html` and ensure line 569 is set for local testing:

```javascript
const API_SERVER_URL = 'http://localhost:3000';
```

## Running the Tests

### Start the Server

```bash
npm start
```

You should see:
```
Server running on port 3000
API available at http://localhost:3000/api/download-schedule
```

### Test Server Health

Open browser and navigate to:
```
http://localhost:3000
```

Expected response:
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

### Test File Download

Navigate to:
```
http://localhost:3000/api/download-schedule
```

This should:
- Download the Excel file, OR
- Show an error message if credentials are incorrect

### Test Frontend Display

1. Open `index.html` in your browser
2. The page should:
   - Show "Loading appointments..." initially
   - Then display appointment data if there are appointments today
   - Or show "No appointments scheduled for today"

## Testing Checklist

- [ ] Server starts without errors
- [ ] Health check endpoint returns correct JSON
- [ ] Download endpoint successfully fetches Excel file
- [ ] Frontend loads without console errors
- [ ] Appointments for today are displayed correctly
- [ ] Order numbers are shown in first column
- [ ] Appointment times are shown in second column
- [ ] Footer shows correct appointment count
- [ ] Last updated time displays correctly
- [ ] Refresh button works
- [ ] Auto-refresh triggers after 5 minutes

## Common Issues

### Port Already in Use

If you see "Port 3000 is already in use":

```bash
# Find process using port 3000
lsof -i :3000

# Kill the process
kill -9 PID
```

Or change the port in `.env`:
```
PORT=3001
```

### SharePoint Authentication Errors

Check:
1. Credentials are correct in `.env`
2. Client secret hasn't expired
3. App has proper SharePoint permissions
4. Tenant ID matches your organization

### Excel File Not Found

Verify:
1. File name is exactly "Appoinement.xlsx"
2. File is in SuniqueKnowledgeBase SharePoint site
3. App has read permissions to the file

### No Appointments Displayed

Check:
1. Open browser console (F12)
2. Look for JavaScript errors
3. Verify Excel file has:
   - A column with "Order" in the header
   - A column with "Appointment Time" in the header
   - A column with date information
4. Confirm there are appointments scheduled for today's date

## Browser Testing

Test in different browsers:
- Chrome (recommended for TV display)
- Firefox
- Safari
- Edge

## Resolution Testing

Test at different resolutions:
- 1920x1080 (Full HD)
- 1366x768 (HD)
- 3840x2160 (4K)

Use browser developer tools (F12) to simulate different screen sizes.

## Performance Testing

1. Open browser developer tools (F12)
2. Go to Network tab
3. Refresh the page
4. Check:
   - API response time
   - Total page load time
   - Any failed requests

Expected metrics:
- API response: < 3 seconds
- Page load: < 5 seconds
- No failed requests

## Next Steps

After successful local testing:
1. Update `API_SERVER_URL` to production Railway URL
2. Deploy to Railway and Netlify
3. Test production deployment
4. Set up TV display

