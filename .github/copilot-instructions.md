# GhostWriter

GhostWriter is a single-file HTML5 web application that provides a rich text editor with Google Drive integration and AI-powered writing assistance via OpenRouter API. The entire application is contained in `index.html` with embedded CSS and JavaScript.

Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.

## Working Effectively

- **No build system required** - This is a pure client-side application with no compilation, dependencies, or build steps
- Run the application locally:
  - `cd /home/runner/work/Ghostwriter/Ghostwriter`
  - `python3 -m http.server 8000` -- starts immediately. NEVER CANCEL.
  - Navigate to `http://localhost:8000` in browser
- Alternative web servers:
  - `node -e "require('http').createServer((req, res) => { res.writeHead(200, {'Content-Type': 'text/html'}); res.end(require('fs').readFileSync('index.html')); }).listen(8000, () => console.log('Server running on port 8000'))"`
  - Any static file server will work
- **Timing**: Server startup is immediate (< 1 second), manual testing takes 5-10 minutes total

## Application Architecture

- **Single file**: `index.html` contains everything (HTML, CSS, JavaScript ~1477 lines)
- **No external dependencies**: All required libraries loaded via CDN
- **Client-side only**: No server-side code or database
- **External integrations**:
  - Google Drive API for file storage and sync
  - Google OAuth for authentication  
  - OpenRouter API for AI writing assistance

## Core Features & Validation

After making changes, ALWAYS test these core scenarios manually:

### Basic Editor Functionality (2 minutes)
1. Start web server and open `http://localhost:8000`
2. Click in the main text area and type some text
3. Test formatting buttons: Bold (Ctrl+B), Italic (Ctrl+I), Underline (Ctrl+U)
4. Test heading dropdown - select different heading levels
5. Test bulleted list button
6. Verify text appears correctly in editor

### Preview and Display Modes (1 minute)
1. Click "Preview" button - should toggle to preview-only mode
2. Click "Split" button - should show side-by-side editor and preview
3. Click "Preview" again to return to edit mode
4. Verify content renders correctly in preview with proper formatting

### Metadata Panel (1 minute)
1. Click "Metadata" button (or press Alt+M)
2. Verify settings panel opens on the right
3. Test tab switching: "Story Settings", "AI Settings", "Display"
4. Enter text in "AI Pre-prompt" field
5. Click "Close" button to close panel

### Authentication Features (Limited Testing)
- Google Sign In button appears but won't work without proper domain setup
- File creation/loading features require authentication
- AI features require OpenRouter API key

## Common Tasks

### Testing Changes
- Always run the local web server after making changes
- Open browser and manually test affected functionality
- Take screenshot if UI changes are made
- Test on both desktop and mobile viewport sizes

### Code Structure
The single `index.html` file contains:
- **Lines 1-400**: HTML structure and CSS styles
- **Lines 400-600**: Application configuration and constants
- **Lines 600-800**: Event handlers and UI logic
- **Lines 800-1200**: Google Drive API integration
- **Lines 1200-1400**: AI generation and OpenRouter integration
- **Lines 1400-1477**: File management and utility functions

### Key JavaScript Functions
- `wireEvents()` - Sets up all event listeners
- `generateAIContent()` - Handles AI writing assistance
- `updatePreview()` - Updates preview pane with formatted content
- `flushSave()` - Saves content to Google Drive
- `loadFile(id)` - Loads file from Google Drive

## Limitations & Important Notes

- **Authentication Required**: Google Drive features only work when properly authenticated with valid domain
- **API Keys**: AI features require OpenRouter API key configuration
- **No Build Process**: Changes to HTML/CSS/JS are immediately reflected (just refresh browser)
- **No Automated Tests**: Manual testing is the only validation method
- **External Dependencies**: Google APIs and OpenRouter must be accessible

## Validation Scenarios

ALWAYS complete these scenarios after making changes:

### Complete User Workflow (5 minutes)
1. Start web server: `python3 -m http.server 8000`
2. Open browser to `http://localhost:8000`
3. Type a sample story: "Once upon a time, there was a brave developer who needed to test an application."
4. Apply formatting: Bold the word "brave", make "developer" italic
5. Add a heading: Select "Once upon a time" and change to H1
6. Test preview: Click Preview button, verify formatting appears correctly
7. Test split view: Click Split button, verify side-by-side layout
8. Open metadata: Click Metadata button, verify panel opens
9. Switch tabs: Click "AI Settings" tab, verify content changes
10. Close metadata: Click Close button, verify panel closes
11. Return to edit mode: Click Preview button to exit preview mode

### Responsive Design Test (2 minutes)
1. Resize browser window to mobile size (320px width)
2. Verify UI remains usable and readable
3. Test all buttons and interactions work on small screen
4. Resize back to desktop size and verify layout

## File Locations

- **Main application**: `/index.html` (single file containing everything)
- **Repository root**: Contains only index.html and .git directory
- **No configuration files**: No package.json, Makefile, or build scripts

## Error Handling

- Console errors about "ERR_BLOCKED_BY_CLIENT" for Google APIs are expected during local testing
- Authentication features will show "Signed out" state during local development  
- Missing API keys will disable AI features but won't break core editor functionality
- Expected console messages during testing:
  - `Failed to load resource: net::ERR_BLOCKED_BY_CLIENT.Inspector @ https://accounts.google.com/...`
  - `Password field is not contained in a form: (More info: https://goo.gl/9p2vKq)`
- These errors do not affect core functionality and can be ignored during development