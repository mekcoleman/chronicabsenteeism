# GitHub Deployment Instructions

## File Size Issue
The complete HTML file with embedded data is **1.5MB**, which is too large for many content management systems and embedding platforms (most have 1MB limits).

## Solution: GitHub Pages Hosting

The GitHub version splits the graphic into two files:
- **chronic_absenteeism_graphic_github.html** (26KB) - The interface
- **school_data.json** (1.5MB) - The data

---

## Deployment Steps

### 1. Create a GitHub Repository

```bash
# Create a new repository on GitHub (via web interface)
# Name it something like: illinois-school-data
```

### 2. Upload Files

Upload these two files to your repository:
- `chronic_absenteeism_graphic_github.html` 
- `school_data.json`

**Option A: Via GitHub Web Interface**
1. Go to your repository
2. Click "Add file" → "Upload files"
3. Drag both files
4. Commit changes

**Option B: Via Git Command Line**
```bash
git clone https://github.com/YOUR-USERNAME/illinois-school-data.git
cd illinois-school-data
# Copy the two files into this directory
git add chronic_absenteeism_graphic_github.html school_data.json
git commit -m "Add Illinois schools chronic absenteeism graphic"
git push origin main
```

### 3. Enable GitHub Pages

1. Go to repository Settings
2. Navigate to "Pages" (left sidebar)
3. Under "Source", select "Deploy from a branch"
4. Select branch: `main` and folder: `/ (root)`
5. Click "Save"

### 4. Access Your Graphic

After a few minutes, your graphic will be available at:
```
https://YOUR-USERNAME.github.io/illinois-school-data/chronic_absenteeism_graphic_github.html
```

---

## Embedding in Your Website

Once hosted on GitHub Pages, you can embed it using an iframe with **automatic height adjustment**:

### Option 1: Auto-Resizing Iframe (Recommended)

```html
<iframe 
    id="school-graphic"
    src="https://YOUR-USERNAME.github.io/illinois-school-data/chronic_absenteeism_graphic_github.html" 
    width="100%" 
    style="border: none; display: block;"
    scrolling="no">
</iframe>

<script>
// Listen for height messages from the iframe
window.addEventListener('message', function(event) {
    if (event.data.type === 'resize') {
        const iframe = document.getElementById('school-graphic');
        iframe.style.height = event.data.height + 'px';
    }
});
</script>
```

**Benefits:**
- Iframe height automatically adjusts as content changes
- No cut-off content
- Works when users search for schools or change subgroups

### Option 2: Fixed Height Iframe (Simple)

```html
<iframe 
    src="https://YOUR-USERNAME.github.io/illinois-school-data/chronic_absenteeism_graphic_github.html" 
    width="100%" 
    height="2000" 
    frameborder="0"
    style="border: none;">
</iframe>
```

**Set height based on typical use:**
- Minimum: 1800px (statewide data only)
- With school selected: 2200px
- Safe default: 2000px

### Option 3: Full-Page Integration

Copy the HTML directly into your page (no iframe) - requires the JSON file to be accessible.

---

## Alternative: Use the Embedded Version

If you have a platform that supports 1.5MB+ files, you can use:
- **chronic_absenteeism_graphic.html** (all-in-one, no external files needed)

This version works standalone without needing GitHub Pages or separate data files.

---

## Files Included

1. **chronic_absenteeism_graphic.html** (1.5MB)
   - Complete standalone version with embedded data
   - Use for: WordPress, direct hosting, local viewing

2. **chronic_absenteeism_graphic_github.html** (26KB)
   - HTML interface only
   - Requires: school_data.json in same directory
   - Use for: GitHub Pages, size-restricted platforms

3. **school_data.json** (1.5MB)
   - Data file with 1,000 schools/districts
   - 11 demographic subgroups per entity
   - Must be in same directory as GitHub HTML version

---

## Troubleshooting

**"Data not loading" error:**
- Ensure both files are in the same directory
- Check that file names are exactly: `school_data.json` (case-sensitive)
- Verify GitHub Pages is enabled and deployed

**Iframe not showing:**
- Increase iframe height
- Check browser console for errors
- Verify the URL is correct and accessible

**Slow loading:**
- First load may take 2-3 seconds (1.5MB data file)
- Subsequent loads are cached and fast
- This is normal for the data size

---

## Updates

To update the data:
1. Replace `school_data.json` in your repository
2. Commit and push changes
3. GitHub Pages will auto-deploy (takes 1-2 minutes)
