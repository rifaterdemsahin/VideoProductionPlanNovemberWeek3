# Prompter Data File

## Overview

The prompter.html page now loads its data dynamically from a structured data file instead of hardcoded HTML. This makes it easier to update content without modifying the HTML structure.

## Files

- **prompter-data.yaml**: The source YAML file containing all video production data
- **prompter-data.json**: JSON version generated from YAML (used by the HTML page)
- **prompter.html**: The main prompter page that loads and displays the data

## Data Structure

The YAML file contains the following sections:

### 1. Project Information
```yaml
project:
  title: "🎬 Video Production Prompter"
  subtitle: "Day 1: AI Starter That Teaches You (No Copy-Paste)"
  runtime: "90 seconds"
  launch: "Tuesday, 18 Nov 2025, 9:00 AM GMT"
```

### 2. Project Details
```yaml
project_info:
  project_name: "Anti-Hype AI Learning Video (Day 1)"
  status: "PRODUCTION READY - TIME CODED"
  owner: "@rifaterdemsahin"
  location: "UK"
  primary_asset: "Delivery Pilot"
  series: "AI Learning Roadmap"
```

### 3. Voice Over Segments
Each segment includes:
- `id`: Segment number
- `time_code`: Timing information
- `text`: Voice-over script text
- `scene`: Scene details including:
  - `title`: Scene description
  - `shot_type`: Camera shot type
  - `fps`: Frame rate
  - `visual_cue`: Visual description
  - `thumbnail`: Thumbnail text

### 4. Production Checklist
Array of checklist items with:
- `text`: Description of the task
- `status`: Either "completed" or "pending"

## Updating Content

### To update the prompter content:

1. **Edit the YAML file** (`prompter-data.yaml`):
   ```bash
   nano prompter-data.yaml
   # or use your preferred editor
   ```

2. **Regenerate the JSON file**:
   ```bash
   python3 -c "import yaml, json; print(json.dumps(yaml.safe_load(open('prompter-data.yaml')), indent=2))" > prompter-data.json
   ```

3. **Test locally**:
   ```bash
   python3 -m http.server 8080
   # Open http://localhost:8080/prompter.html in your browser
   ```

4. **Commit and push changes**:
   ```bash
   git add prompter-data.yaml prompter-data.json
   git commit -m "Update prompter data"
   git push
   ```

## Why YAML and JSON?

- **YAML** is human-readable and easy to edit, making it ideal for content updates
- **JSON** has native browser support and doesn't require external libraries
- We maintain both files: YAML as the source of truth, JSON for browser consumption

## Features Preserved

All original prompter features remain functional:
- ✅ Auto-scroll functionality
- ✅ Keyboard shortcuts (Arrow keys, Home, Enter, Space)
- ✅ Visual segment highlighting
- ✅ Scroll indicator
- ✅ Responsive design
- ✅ Project information display
- ✅ Production checklist

## Technical Implementation

The prompter.html uses JavaScript's `fetch()` API to load the JSON file asynchronously and dynamically renders all content using the `renderContent()` function. This separation of content and presentation makes the system more maintainable and scalable.
