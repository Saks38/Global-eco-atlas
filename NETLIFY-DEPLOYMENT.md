# Quick Netlify Upload Instructions

## After Building (npm run build)

1. **Go to the `dist/public` folder**
2. **Select ALL files inside**:
   - `index.html`
   - `assets` folder
   - `favicon.svg` 
   - `_redirects`
3. **Drag these files to Netlify** (not the folder itself)

## Key Point
✅ Upload the **contents** of `dist/public`
❌ Don't upload the `dist` or `dist/public` folder

The files should appear at the root level on Netlify, not in subfolders.