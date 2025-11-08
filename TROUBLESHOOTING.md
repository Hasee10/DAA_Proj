# Troubleshooting Guide

## Blank White Screen

### Symptoms
- Browser shows completely blank white screen
- URL is `localhost:5000`
- No content is displayed

### Possible Causes & Solutions

#### 1. JavaScript Error
**Check:**
- Open browser DevTools (F12)
- Go to Console tab
- Look for red error messages

**Common errors:**
- `Cannot read property of undefined` - Data structure mismatch
- `SyntaxError` - Invalid JavaScript syntax
- `React is not defined` - CDN not loading

**Fix:**
- Check that React libraries are loading from CDN
- Clear browser cache and reload (Ctrl+F5)
- Check that all files are saved properly

#### 2. Backend Not Running
**Check:**
- Backend terminal should show: `Running on http://0.0.0.0:5000`
- Try accessing `http://localhost:5000/api/health` directly

**Fix:**
```powershell
cd backend
python app.py
```

#### 3. Port Conflicts
**Check:**
- Another application using port 5000
- Check error: `Port 5000 is already in use`

**Fix:**
- Stop other application or change port in `app.py` line 277:
```python
app.run(debug=True, host='0.0.0.0', port=5001)
```

#### 4. File Not Serving
**Check:**
- In browser DevTools → Network tab
- Refresh page
- Look for `index.html` - should return 200 status

**Fix:**
- Verify file path in `app.py` line 12:
```python
app = Flask(__name__, static_folder='../frontend', static_url_path='')
```

## Analysis Button Doesn't Work

### Symptoms
- Button appears grayed out
- Clicking does nothing
- "Start Analysis" button remains disabled

### Solutions

#### 1. No Job Description Selected
- Must click on a job description card (Data Scientist, Web Developer, or Software Tester)
- Selected card will show purple border

#### 2. No Files Uploaded
- Must upload at least one CV file
- File should appear in "Uploaded Files" section with green checkmark

#### 3. Browser Console Errors
- Open DevTools (F12) → Console
- Look for errors when clicking the button
- Check Network tab for failed API calls

## Results Not Displaying

### Symptoms
- Click "Start Analysis" but page stays blank
- Goes to Results tab but shows "No Analysis Results Yet"

### Solutions

#### 1. Check Backend Logs
In terminal running `python app.py`, look for:
- `ERROR:` messages
- `Traceback` errors
- Check if files are being processed

#### 2. Check Browser Console
- Open DevTools (F12) → Console
- Look for API errors
- Check Network tab → `/api/analyze` request

#### 3. File Upload Issues
- Check `backend/uploads/` folder exists
- Files should be saved there after upload
- Verify file format (PDF, DOCX, or TXT)

#### 4. Backend Processing Error
- Check if CV text is being extracted properly
- Might fail if CV is corrupt or unsupported format
- Check backend terminal for error messages

## Debugging Steps

### Step 1: Check if Backend is Running
```powershell
# In terminal
cd backend
python app.py
```
Should see: `Server starting on http://localhost:5000`

### Step 2: Check Browser Console
1. Press F12 to open DevTools
2. Go to Console tab
3. Look for any red error messages
4. Share error message with developer

### Step 3: Test API Endpoint
Visit in browser: `http://localhost:5000/api/health`
Should return: `{"status": "healthy", "message": "CV Analyzer API is running"}`

### Step 4: Check File Upload
1. Upload a CV file
2. Check browser console for upload errors
3. Check `backend/uploads/` folder has the file

### Step 5: Test Analysis
1. Select a job description
2. Upload at least one CV
3. Click "Start Analysis"
4. Check browser console for API call details
5. Check backend terminal for processing errors

## Common Error Messages

### "ERROR: cv_processor.py"
- CV file cannot be read
- File might be corrupted or wrong format
- **Fix:** Try a different CV file

### "No files provided"
- File upload failed
- **Fix:** Re-upload files, check file size < 16MB

### "Missing required data"
- Backend didn't receive all needed information
- **Fix:** Check that job description and CV files are selected

### "can't read property 'map' of undefined"
- Frontend expecting data that backend didn't provide
- **Fix:** Check browser console for exact error location

## Getting Help

If issues persist:
1. Copy error message from browser console
2. Copy error from backend terminal
3. Screenshot the browser showing the issue
4. Check that all files were saved properly
5. Try restarting backend server

## Quick Reset

If nothing works, try:
```powershell
# Stop backend (Ctrl+C in terminal)

# Delete uploads folder
cd backend
Remove-Item -Recurse -Force uploads

# Restart backend
python app.py

# Clear browser cache
# Press Ctrl+Shift+Delete
# Select "Cached images and files"
# Clear and restart browser
```
