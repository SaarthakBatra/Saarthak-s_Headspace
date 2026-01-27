# cPanel Portfolio Setup Guide - Metadrix.com
## Complete Step-by-Step Instructions for Subdirectories

**Timeline:** 30-45 minutes total  
**Goal:** Upload 4 projects to `metadrix.com/portfolio/project1`, `project2`, `project3`, `project4`

---

## PHASE 1: Access cPanel & Create Directory Structure (5 minutes)

### Step 1.1: Log into cPanel
1. Open browser and go to: `https://premium907.web-hosting.com:2083`
   - *(Or use your cPanel login URL - check your Namecheap welcome email if unsure)*
2. Username: `metazqwq` (from your screenshot)
3. Password: *(Your cPanel password)*
4. Click **Login**

### Step 1.2: Open File Manager
1. In cPanel dashboard, find **Files** section
2. Click **File Manager**
3. A new window opens showing your server files
4. You should see a folder list with `public_html` folder (this is your website root)
5. Click on `public_html` to enter it

### Step 1.3: Create Portfolio Directory
1. Inside `public_html`, right-click in empty space
2. Select **Create New Folder**
3. Name it: `portfolio` (lowercase)
4. Click **Create New Folder** button
5. ✅ You now have `/public_html/portfolio/`

### Step 1.4: Create Project Subdirectories
Repeat this 4 times for each project:

1. Double-click to enter the `portfolio` folder
2. Right-click in empty space
3. Select **Create New Folder**
4. Name it: `project1` (first project)
5. Click **Create New Folder**

*Repeat for:*
- `project2`
- `project3`
- `project4`

**Result:** You now have this structure:
```
/public_html/
  └── portfolio/
      ├── project1/
      ├── project2/
      ├── project3/
      └── project4/
```

---

## PHASE 2: Prepare Your Project Files (10 minutes)

Before uploading, prepare each project on your local computer:

### Step 2.1: Organize Each Project Folder
For **each project**, you should have a folder like this locally:
```
project1/
  ├── index.html
  ├── css/
  │   └── styles.css
  ├── js/
  │   └── script.js
  ├── images/
  │   └── (all images)
  └── (any other assets)
```

**Important:** Every project folder MUST have an `index.html` at the root level.

### Step 2.2: Zip Each Project (Recommended for Upload Speed)
1. Right-click your `project1` folder on your computer
2. Select **Send to → Compressed (zipped) folder**
3. This creates `project1.zip`
4. Repeat for `project2`, `project3`, `project4`

You now have:
- `project1.zip`
- `project2.zip`
- `project3.zip`
- `project4.zip`

*Note: If your files are small (<50MB per project), you can skip zipping and upload directly.*

---

## PHASE 3: Upload Projects via cPanel (20-30 minutes)

### Step 3.1: Upload First Project (Project1)

**In cPanel File Manager (keep it open from Phase 1):**

1. Navigate to: `/public_html/portfolio/project1/`
   - Double-click `portfolio` folder
   - Double-click `project1` folder
   - You should be inside the empty `project1` folder

2. Click **Upload** button (top menu bar)

3. **If uploading ZIP file:**
   - Drag `project1.zip` into the upload area (or click to browse and select it)
   - Wait for upload to complete (progress bar shows)
   - Once done, right-click `project1.zip` → **Extract**
   - Select destination: current folder (`project1`)
   - Click **Extract File(s)**
   - Delete the `project1.zip` file (right-click → Delete)

4. **If uploading unzipped files:**
   - Select all files/folders from your local `project1` folder
   - Drag them into the upload area in cPanel
   - Or use file browser to select multiple files
   - Wait for upload to complete

5. ✅ Verify: Inside `project1` folder you should now see:
   - `index.html`
   - `css/`, `js/`, `images/` folders
   - All other project files

### Step 3.2: Repeat for Project2, Project3, Project4

For each remaining project:

1. Navigate back to: `/public_html/portfolio/`
2. Double-click into `project2` folder
3. Repeat Step 3.1 process (upload → extract if zipped → verify)
4. Repeat for `project3` and `project4`

**Total files uploaded:** 4 complete project structures

---

## PHASE 4: Test & Configure Redirects (10 minutes)

### Step 4.1: Test Each Project
1. Open browser and visit:
   - `https://metadrix.com/portfolio/project1`
   - `https://metadrix.com/portfolio/project2`
   - `https://metadrix.com/portfolio/project3`
   - `https://metadrix.com/portfolio/project4`

2. Each should display your project's `index.html` page
3. Click around - verify all links, images, scripts load correctly
4. Check responsive design on mobile

**If a project doesn't load:**
- Check that `index.html` exists in that folder
- Check browser console (F12) for error messages
- Verify file names and paths match your code

### Step 4.2: Create a Portfolio Index (Optional but Recommended)

To make `metadrix.com/portfolio` show a list of projects:

1. Navigate to `/public_html/portfolio/` in cPanel File Manager
2. Click **Create New File**
3. Name it: `index.html`
4. Click **Create**
5. Right-click the file → **Edit**
6. Add this HTML:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Metadrix Portfolio</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f5f5f5;
            padding: 40px 20px;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        .portfolio-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }
        .project-card {
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
            text-align: center;
        }
        .project-card a {
            display: inline-block;
            margin-top: 15px;
            padding: 10px 20px;
            background: #007bff;
            color: white;
            text-decoration: none;
            border-radius: 4px;
        }
        .project-card a:hover {
            background: #0056b3;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Metadrix Portfolio</h1>
        <p style="text-align: center; color: #666;">Our Featured Projects</p>
        
        <div class="portfolio-grid">
            <div class="project-card">
                <h3>Project 1</h3>
                <p>Description of your first project</p>
                <a href="/portfolio/project1">View Project →</a>
            </div>
            
            <div class="project-card">
                <h3>Project 2</h3>
                <p>Description of your second project</p>
                <a href="/portfolio/project2">View Project →</a>
            </div>
            
            <div class="project-card">
                <h3>Project 3</h3>
                <p>Description of your third project</p>
                <a href="/portfolio/project3">View Project →</a>
            </div>
            
            <div class="project-card">
                <h3>Project 4</h3>
                <p>Description of your fourth project</p>
                <a href="/portfolio/project4">View Project →</a>
            </div>
        </div>
    </div>
</body>
</html>
```

7. Click **Save**

### Step 4.3: Redirect metadrix.com Home to Portfolio (Remove Parking Page)

1. In cPanel, go back to main dashboard
2. Find **Domains** section
3. Click on your domain `metadrix.com`
4. Look for **Redirects** or **Manage Domain**
5. Set redirect: `metadrix.com` → `metadrix.com/portfolio`

**Alternative method (if redirect not available):**

1. In File Manager, navigate to `/public_html/`
2. If `index.html` exists, delete or rename it
3. Create new `index.html` with this code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="refresh" content="0; url=/portfolio/">
</head>
<body>
    <p>Redirecting to portfolio...</p>
</body>
</html>
```

4. Save and test: `metadrix.com` should now redirect to `metadrix.com/portfolio`

---

## PHASE 5: Troubleshooting Checklist

### Projects Not Displaying?

**Issue:** Getting 404 error
- ✅ Verify `index.html` exists in each project folder
- ✅ Check file names are exactly lowercase: `index.html` (not `Index.html`)
- ✅ Verify correct folder structure uploaded

**Issue:** Images/CSS/JS not loading
- ✅ Check browser console (F12) for errors
- ✅ Verify file paths in HTML are correct (use relative paths: `./css/style.css` or `css/style.css`)
- ✅ Don't use absolute paths starting with `/` unless your files are truly in root

**Issue:** Takes 30+ seconds to load
- ✅ Shared hosting can be slow sometimes
- ✅ Compress images to reduce file size
- ✅ Minify CSS/JS if using large libraries

### Permission Issues?

- In cPanel File Manager, right-click folder → **Change Permissions**
- Set to: `755` (standard web directory permission)
- Apply recursively to all files

---

## QUICK REFERENCE: Your Live URLs

Once complete, these will be live:

```
🌐 Main Portfolio:     https://metadrix.com/portfolio
🌐 Project 1:         https://metadrix.com/portfolio/project1
🌐 Project 2:         https://metadrix.com/portfolio/project2
🌐 Project 3:         https://metadrix.com/portfolio/project3
🌐 Project 4:         https://metadrix.com/portfolio/project4
```

---

## ADDING NEW PROJECTS MONTHLY

When you add a 5th project next month:

1. Open cPanel File Manager
2. Navigate to `/public_html/portfolio/`
3. Create new folder: `project5`
4. Upload files (same process as Phase 3)
5. Update portfolio index if you created one
6. **Done** — no code changes needed

---

## FILE PERMISSIONS REFERENCE

| Item | Permission | What It Means |
|------|-----------|---|
| Folders | 755 | Readable by all, writable by owner |
| HTML/CSS/JS files | 644 | Readable by all, writable by owner |
| CGI scripts | 755 | Executable by server |

*Most files are 644 by default — usually fine. Only change if you get permission errors.*

---

## SUPPORT RESOURCES

**If you get stuck:**
1. cPanel Help: Click **Help** icon in top-right of cPanel
2. Check file paths — 90% of issues are path-related
3. Check browser console (F12 → Console) for error messages
4. Verify all files uploaded successfully (sometimes large files timeout)

---

**You're ready to go! Questions on any specific step?**