# Netlify Deployment Guide

## Clean Project Structure

The project has been cleaned and reorganized with the following structure:

```
/
├── client/                 # Frontend source code
│   ├── src/               # React components and pages
│   ├── public/            # Static assets
│   └── index.html         # Main HTML template
├── server/                # Backend source code
│   ├── index.ts           # Main server file
│   ├── routes.ts          # API routes
│   ├── storage.ts         # Data storage interface
│   └── vite.ts            # Vite server integration
├── shared/                # Shared types and schemas
│   └── schema.ts          # Database schema and types
├── dist/                  # Build output (created after npm run build)
│   ├── index.js           # Built server
│   └── public/            # Built frontend (ready for Netlify)
├── netlify.toml           # Netlify configuration
├── package.json           # Dependencies and scripts
└── vite.config.ts         # Build configuration
```

## How to Deploy to Netlify

### Step 1: Build the Project
```bash
npm run build
```

### Step 2: Upload to Netlify
After building, go to the `dist/public` folder and upload **only the contents** to Netlify:

Required files for upload:
- `index.html`
- `assets/` folder (contains CSS and JS)
- `favicon.svg`
- `_redirects`

### Step 3: Verify Deployment
Test these URLs on your deployed site:
- Main page: `/`
- Calculator: `/calculator`
- Stories: `/stories`
- All should work without 404 errors

## Configuration Files

### netlify.toml
- Sets build command and publish directory
- Configures redirects for React routing
- Adds security headers

### _redirects (in public folder)
- Handles client-side routing
- Ensures direct navigation works

## Important Notes

- Upload **contents** of `dist/public`, not the folder itself
- The `_redirects` file prevents 404 errors for direct navigation
- All JavaScript and CSS is bundled and optimized
- No server functionality on Netlify (frontend only)