# CLAUDE.md - AI Assistant Guide

This file provides guidance for AI assistants working with the Google Chat Takeout Reader codebase.

## Project Overview

**Google Chat Takeout Reader** is a lightweight, single-file web utility for viewing Google Chat data exported via Google Takeout. All processing occurs client-side in the browser with no server involvement.

- **Repository**: `mrwoof/google-chat-takeout-reader`
- **Live URL**: https://mrwoof.github.io/google-chat-takeout-reader/google_chat_takeout_reader.html
- **License**: MIT

## Codebase Structure

```
google-chat-takeout-reader/
├── google_chat_takeout_reader.html  # The entire application (single file)
├── README.md                         # User-facing documentation
├── LICENSE                           # MIT License
├── CLAUDE.md                         # This file
└── static/img/
    └── chat-reader-logo.png         # Application logo
```

This is an intentionally minimal project. The entire application lives in a single HTML file with embedded CSS and JavaScript.

## Main Application File Structure

`google_chat_takeout_reader.html` is organized as:

| Section | Lines | Purpose |
|---------|-------|---------|
| CSS Styles | 8-108 | Custom styling for chat UI, thumbnails, reactions |
| HTML Structure | 114-131 | Two-column Bootstrap layout |
| JavaScript | 133-462 | All application logic |

### Key JavaScript Data Structures

```javascript
let chatMetadataEntries = {};  // Chat metadata (members, names) keyed by chat ID
let chatMessageFiles = {};      // Maps chat IDs to message file entries
let fileCache = {};             // Caches file objects for image retrieval
let imgCache = {};              // Tracks image filename occurrences for duplicates
let chatMessageCache = {};      // Caches parsed message JSON
```

### Core Functions

| Function | Purpose |
|----------|---------|
| `pickDirectory()` | Opens browser directory picker dialog |
| `listFilesRecursive()` | Traverses directory tree to find chat files |
| `addChatMetadataEntry()` | Parses `group_info.json` files |
| `addChatMessagesEntry()` | Locates `messages.json` files |
| `readAndDisplayJsonFile()` | Renders messages with filtering/pagination |
| `formatTimestamp()` | Converts Takeout date format to locale strings |
| `convertImageFilename()` | Handles filename escaping and duplicate detection |
| `goToMessage()` | Navigates to specific message number |

## Technology Stack

- **HTML5/CSS3/Vanilla JavaScript** - No frameworks
- **jQuery 3.6.0** - DOM manipulation (CDN)
- **Bootstrap 5.3.0** - UI components (CDN)
- **File System Access API** - Directory picking (`window.showDirectoryPicker()`)

## Development Workflow

### No Build System

This project requires **no build process**. Changes are made directly to the HTML file.

### Running Locally

1. Open `google_chat_takeout_reader.html` directly in Google Chrome
2. Or serve via any static file server

### Browser Requirements

- **Google Chrome required** - The File System Access API (`window.showDirectoryPicker()`) only works in Chrome/Chromium browsers
- Firefox, Safari, Edge do not support this API

## Code Conventions

### Naming

- **camelCase** for all functions and variables
- Descriptive names: `getChatMembersTitle()`, `preprocessImages()`, `formatTimestamp()`
- ID prefixes for dynamic elements: `opts-${chatId}`, `imagesOnly-${chatId}`

### Patterns

- Object-based state management via global caches
- Async/await for file I/O operations
- Template literals for dynamic HTML generation
- jQuery for DOM manipulation and event handling
- Try-catch with console logging for error handling

### Performance

- Messages displayed in chunks of 5,000 max
- Pagination to prevent DOM overwhelm
- File and image caching to avoid re-parsing

## Google Takeout Data Format

The application expects this structure:

```
Takeout/
└── Google Chat/
    └── Groups/
        └── [Chat Name]/
            ├── messages.json     # Message array with text, attachments, reactions
            ├── group_info.json   # Member list and chat name
            └── [images]          # Attached image files
```

### Key JSON Structures

**messages.json**:
```json
{
  "messages": [{
    "creator": { "name": "User Name", "email": "user@example.com" },
    "created_date": "Thursday, July 14, 2016 at 5:04:34 PM UTC",
    "text": "Message content",
    "attached_files": [{ "export_name": "image.jpg" }],
    "reactions": [{ "emoji": { "unicode": "👍" }, "reactor_emails": ["user@example.com"] }]
  }]
}
```

**group_info.json**:
```json
{
  "name": "Chat Name",
  "members": [{ "name": "User", "email": "user@example.com" }]
}
```

## Common Tasks

### Adding a New Feature

1. All code goes in `google_chat_takeout_reader.html`
2. Add CSS in the `<style>` block (lines 8-108)
3. Add HTML in the `<body>` section (lines 114-131)
4. Add JavaScript after line 133

### Modifying Message Display

The `readAndDisplayJsonFile()` function handles all message rendering. Key sections:
- Message filtering logic
- HTML template generation for each message
- Image/attachment handling
- Reaction display

### Adding New Filters

1. Add checkbox in the dynamically generated form (inside `readAndDisplayJsonFile()`)
2. Check the filter value when processing messages
3. Update the message display logic accordingly

## Testing

**No automated tests exist.** Manual testing workflow:

1. Download sample Google Chat Takeout data
2. Open the HTML file in Chrome
3. Select the Takeout directory
4. Verify chats display correctly
5. Test filters, pagination, and image display

## Important Notes for AI Assistants

1. **Single-file architecture**: All changes go in one HTML file. Keep this simplicity.

2. **No dependencies to install**: Uses CDN-hosted jQuery and Bootstrap. No npm, no package.json.

3. **Chrome-only**: Don't suggest cross-browser compatibility for the File System Access API - it's intentionally Chrome-only.

4. **Privacy-first**: No server-side components. Don't add any external data transmission.

5. **Inline styles and scripts**: This is by design for a single-file utility. Don't extract to separate files unless explicitly requested.

6. **Image handling quirks**: The `convertImageFilename()` function handles Google's filename escaping (`?:` replacement) and duplicate filename tracking.

7. **Date format**: Google Takeout uses a specific format like "Thursday, July 14, 2016 at 5:04:34 PM UTC" - the `formatTimestamp()` function handles parsing this.

## Git Workflow

```bash
# View recent changes
git log --oneline -10

# Check status
git status

# Standard commit workflow
git add .
git commit -m "descriptive message"
git push origin <branch-name>
```

## Quick Reference

| What | Where |
|------|-------|
| Main app | `google_chat_takeout_reader.html` |
| CSS styles | Lines 8-108 |
| HTML structure | Lines 114-131 |
| JavaScript | Lines 133-462 |
| Data structures | Lines 134-138 |
| Core display function | `readAndDisplayJsonFile()` |
| Directory picker | `pickDirectory()` |
