# Vercel Deployment - Main Branch

## ✅ Status: Ready to Deploy from Main Branch

All changes have been merged to `main` branch and are ready for Vercel deployment.

## Quick Deploy Commands

### Option 1: Vercel Dashboard (Recommended)

1. **Go to**: https://vercel.com/new
2. **Import Repository**: `jadaunaryansingh/Legally`
3. **Select Branch**: `main`
4. **Add Environment Variables**:
   ```
   HF_TOKEN = (get from your .env file)
   HF_MODEL_ID = AdaptLLM/law-LLM
   VITE_API_BASE_URL = (leave empty)
   VITE_API_PREFIX = /api
   ```
5. **Deploy**: Click "Deploy"

### Option 2: Vercel CLI

```bash
# Install Vercel CLI (if not installed)
npm install -g vercel

# Login
vercel login

# Deploy from main branch
vercel --prod
```

## Environment Variables Setup

**IMPORTANT**: Add these in Vercel Dashboard → Settings → Environment Variables:

1. `HF_TOKEN` - Your Hugging Face token (from `.env` file)
2. `HF_MODEL_ID` - `AdaptLLM/law-LLM` (optional, has default)
3. `VITE_API_BASE_URL` - Leave empty (uses relative URLs)
4. `VITE_API_PREFIX` - `/api`

Set for: **Production**, **Preview**, and **Development** environments.

## Project Configuration

- **Build Command**: `pnpm run build:client`
- **Output Directory**: `dist/spa`
- **Python Runtime**: `python3.11`
- **API Routes**: `/api/*` → FastAPI serverless function
- **Framework**: Vite + React SPA

## Post-Deployment

After deployment, your app will be available at:
- **Production**: `https://your-project.vercel.app`

Test endpoints:
- Homepage: `https://your-project.vercel.app`
- API: `https://your-project.vercel.app/api/legal-advice`
- Chat: Test the chat functionality

## Troubleshooting

### Build Issues
- Check Vercel build logs
- Verify `pnpm` is detected (Vercel auto-detects)
- Ensure all dependencies are in `package.json` and `api/requirements.txt`

### API Not Working
- Verify `HF_TOKEN` is set correctly
- Check function logs in Vercel Dashboard
- Ensure `mangum` is in `api/requirements.txt`

### Environment Variables
- Must be set for all environments (Production, Preview, Development)
- Variable names are case-sensitive
- Redeploy after adding new variables

