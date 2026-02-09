# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-page HTML application for managing party RSVPs. The entire application is contained in `index.html` - a self-contained file with embedded CSS and JavaScript.

## Architecture

**Single-file structure:**
- HTML structure for the invitation page
- Inline `<style>` block with all CSS (dark theme, responsive design)
- Inline `<script>` block with vanilla JavaScript for all functionality

**Key components:**
1. **Guest identification**: URL parameter `?id=<guestId>` identifies invited guests
2. **Google Apps Script backend**: Communicates with `SCRIPT_URL` constant (line 392) for:
   - Fetching guest information (`getGuest` action)
   - Retrieving previous responses (`getResponse` action)
   - Submitting RSVPs (POST request)
3. **Dynamic form behavior**:
   - Conditional field visibility based on attendance selection
   - Plus-one name field appears only when "Yes" selected for +1
   - All fields except attendance hidden when "No" selected for attendance

## Development Commands

**Local development:**
```bash
# Open in browser directly (file:// protocol works but won't make API calls)
open index.html

# For testing with backend API calls, serve with a local server:
python3 -m http.server 8000
# Then open http://localhost:8000
```

**Deployment:**
This is a static HTML file designed to be hosted directly. No build process required.

## Important Constants

- `SCRIPT_URL` (line 392): Google Apps Script endpoint - do not commit changes to this unless intentional
- Guest ID is passed via URL query parameter: `?id=<guestId>`

## Code Patterns

**API communication:**
- All backend calls go through the Google Apps Script URL
- GET requests for fetching data (guest info, previous responses)
- POST requests for submitting RSVPs
- Response format: `{ success: boolean, data/error: ... }`

**State management:**
- Two global variables track current state: `guestId` and `guestName`
- Form state managed through DOM manipulation
- No external libraries or frameworks used

**Error handling:**
- Invalid/missing guest ID shows error page
- Network errors display user-friendly messages
- Console logging for debugging
