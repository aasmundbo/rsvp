# Party RSVP Front-End

Single-page application for managing party RSVPs with unique guest invitation links.

## Overview

Static HTML invitation and RSVP system. Each guest receives a unique URL. Integrates with a Google Apps Script backend for data management.

## Features

- Unique URL per guest with pre-filled name
- Dynamic form fields based on user selections
- Previous responses are loaded and can be updated
- Responsive design for mobile and desktop
- Single HTML file, no build process required

## Technology

- HTML5, CSS3, vanilla JavaScript
- Google Apps Script backend (separate repository)

## Usage

Guest invitation URL format:
```
https://yoursite.com/index.html?id=<unique-guest-id>
```

### Development

**Direct file opening:**

```bash
open index.html
```

Note: Backend API calls will not work with `file://` protocol.

**Local server:**

```bash
# Python 3
python3 -m http.server 8000

# Node.js (with http-server)
npx http-server -p 8000
```

Navigate to `http://localhost:8000`

## Deployment

Static HTML file. Deploy to any web hosting service:
- **GitHub Pages**: Enable in repository settings
- **Netlify/Vercel**: Connect repository, use default settings
- **Traditional hosting**: Upload `index.html`

## Configuration

Backend endpoint configured on line 392:

```javascript
const SCRIPT_URL = 'https://script.google.com/macros/s/[your-script-id]/exec';
```

### Backend API

**GET requests:**

- `?action=getGuest&id=<guestId>` - Returns guest name
- `?action=getResponse&id=<guestId>` - Returns previous RSVP if exists

**POST requests:**

- Body: JSON with RSVP data (id, email, attending, plusOne, plusOneName, dietary)
- Returns: `{ success: boolean, message: string }`

## Project Structure

```text
party-signup-front-end/
├── index.html          # Complete application (HTML + CSS + JS)
├── CLAUDE.md          # Development guidance for Claude Code
└── README.md          # This file
```

## Form Fields

- **Attending**: Yes/No selection (required)
- **Plus One**: Yes/No selection (required if attending)
- **Plus One Name**: Text input (required if bringing +1)
- **Email**: Email address (required if attending)
- **Dietary Restrictions**: Free text (optional)

## Browser Support

Requires JavaScript enabled. Tested on Chrome, Firefox, Safari, Edge.
