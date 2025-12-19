# Vercel Deployment - Final Commands

## Project Status
- **Repository**: https://github.com/jadaunaryansingh/Legally
- **Current Branch**: `Agents`
- **Remote**: Already connected to GitHub ✅

## Environment Variables (from .env file)
Your `.env` file contains:
```
HF_TOKEN=your_huggingface_token_here
HF_MODEL_ID=AdaptLLM/law-LLM
VITE_API_BASE_URL=
VITE_API_PREFIX=/api
```

## Step 1: Commit Current Changes

```bash
# Add all changes
git add .

# Commit with descriptive message
git commit -m "Configure Vercel deployment: Add Mangum handler, update API URLs, add Vercel config files"

# Push to GitHub
git push origin Agents
```

## Step 2: Deploy to Vercel

### Option A: Via Vercel Dashboard (Recommended for First Time)

1. **Go to**: https://vercel.com/new
2. **Import Git Repository**: 
   - Click "Import Git Repository"
   - Select: `jadaunaryansingh/Legally`
   - Branch: `Agents`
3. **Configure Project**:
   - Framework Preset: **Other** (or Vite if available)
   - Root Directory: `./` (root)
   - Build Command: `pnpm run build:client` (auto-detected)
   - Output Directory: `dist/spa` (auto-detected)
4. **Environment Variables** (IMPORTANT - Add these):
   ```
   HF_TOKEN = your_huggingface_token_here (get from .env file)
   HF_MODEL_ID = AdaptLLM/law-LLM
   VITE_API_BASE_URL = (leave empty)
   VITE_API_PREFIX = /api
   ```
5. **Deploy**: Click "Deploy"

### Option B: Via Vercel CLI

```bash
# Install Vercel CLI (if not installed)
npm install -g vercel

# Login to Vercel
vercel login

# Link to existing project (if already deployed) or create new
vercel link

# Set environment variables
vercel env add HF_TOKEN
# When prompted, paste your Hugging Face token from .env file
# Select: Production, Preview, Development (all three)

vercel env add HF_MODEL_ID
# When prompted, paste: AdaptLLM/law-LLM
# Select: Production, Preview, Development (all three)

# Deploy to preview
vercel

# Deploy to production
vercel --prod
```

## Step 3: Verify Deployment

After deployment, test these URLs:

1. **Homepage**: `https://your-project.vercel.app`
2. **API Health Check**: `https://your-project.vercel.app/api/legal-advice` (should show FastAPI docs or error)
3. **Chat Functionality**: Test the chat feature on the homepage

## Important Notes

1. **Python Runtime**: Vercel will use Python 3.11 for the API function (configured in `vercel.json`)
2. **Dependencies**: 
   - Node.js dependencies: Installed via `pnpm install --frozen-lockfile`
   - Python dependencies: Installed from `api/requirements.txt`
3. **API Routes**: 
   - All `/api/*` requests are routed to `api/index.py` (FastAPI serverless function)
   - Frontend uses relative URLs in production (`/api/legal-advice`)
4. **SPA Routing**: All non-API routes serve `index.html` for React Router

## Troubleshooting

### Build Fails
- Check Vercel build logs
- Verify `pnpm` is available (Vercel auto-detects)
- Ensure `package.json` has correct build scripts

### API Not Working
- Verify environment variables are set in Vercel Dashboard
- Check function logs in Vercel Dashboard → Functions tab
- Ensure `api/requirements.txt` includes all dependencies (mangum, fastapi, etc.)

### Environment Variables Not Loading
- Make sure variables are set for **all environments** (Production, Preview, Development)
- Variable names must match exactly (case-sensitive)
- Redeploy after adding new environment variables

## Quick Deploy Commands Summary

```bash
# 1. Commit and push
git add .
git commit -m "Deploy to Vercel"
git push origin Agents

# 2. Deploy (if using CLI)
vercel --prod
```

## Project Structure for Vercel

```
Legally/
├── api/
│   ├── index.py          # FastAPI serverless function entry
│   └── requirements.txt  # Python dependencies
├── client/               # React SPA
├── fastapi_server/       # FastAPI app source
├── vercel.json          # Vercel configuration
└── .env                  # Local env (not deployed, use Vercel Dashboard)
```

