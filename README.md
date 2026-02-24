# M&A Monitor — Western European Public Offers Tracker

Live tracker of all pending public offers across Western Europe, powered by M&A Monitor's deal intelligence.

## Setup (one-time)

### 1. Create a GitHub repository

1. Go to [github.com/new](https://github.com/new)
2. Name it something like `european-public-offers` (or whatever you prefer)
3. Set it to **Public** (required for free GitHub Pages)
4. Click **Create repository**

### 2. Push these files to the repository

```bash
cd github-tracker
git init
git add .
git commit -m "Initial tracker"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/european-public-offers.git
git push -u origin main
```

### 3. Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** → **Pages** (left sidebar)
3. Under "Source", select **Deploy from a branch**
4. Select **main** branch, **/ (root)** folder
5. Click **Save**
6. Wait 1-2 minutes — your site will be live at:
   `https://YOUR_USERNAME.github.io/european-public-offers/`

### 4. (Optional) Custom domain

If you want something like `tracker.mamonitor.com`:

1. In your domain's DNS settings, add a CNAME record:
   - Name: `tracker` 
   - Value: `YOUR_USERNAME.github.io`
2. In GitHub repo Settings → Pages → Custom domain, enter `tracker.mamonitor.com`
3. Check "Enforce HTTPS"

## Updating the data

Whenever you want to refresh the tracker with new data:

```bash
# 1. Export bid premia from M&A Monitor DataBase as xlsx
# 2. Copy/rename it to bid_premia_latest.xlsx in this folder
# 3. Run the update script:
python update_tracker.py

# 4. Push to GitHub (goes live in ~1 minute):
git add .
git commit -m "Data update"
git push
```

That's it. The Python script reads your xlsx, extracts all Western European pending deals, and regenerates `index.html` with the fresh data.

## Updating the news ticker

The "Recent Developments" ticker is currently hardcoded in the HTML. To update it:

1. Open `index.html` (or `template.html`)
2. Find the `const updates=[` section near the bottom
3. Edit the entries — each one has a date, country code, target name, and text
4. Save, commit, push

Alternatively, you could modify `update_tracker.py` to read ticker updates from a separate file (CSV, JSON, etc.) if you prefer.

## File structure

```
├── index.html              ← The live tracker page (auto-generated)
├── template.html           ← Design template (edit this for layout changes)
├── update_tracker.py       ← Python script to refresh data from xlsx
├── bid_premia_latest.xlsx  ← Your latest data export (not committed to git)
├── .gitignore              ← Excludes xlsx files from git
└── README.md               ← This file
```

## Requirements

- Python 3.7+
- openpyxl (`pip install openpyxl`)
