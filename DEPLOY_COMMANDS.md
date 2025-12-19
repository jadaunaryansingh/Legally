# Quick Deployment Commands for Vercel

## Current Git Status
- **Branch**: `Agents`
- **Modified Files**: `client/pages/Laws.tsx` (and other changes)

## Pre-Deployment Checklist

1. **Commit your changes**:
   ```bash
   git add .
   git commit -m "Prepare for Vercel deployment"
   ```

2. **Push to remote** (if not already pushed):
   ```bash
   git push origin Agents
   ```

## Vercel Deployment Commands

### Option 1: Deploy via Vercel CLI (Recommended)

1. **Install Vercel CLI** (if not installed):
   ```bash
   npm install -g vercel
   ```

2. **Login to Vercel**:
   ```bash
   vercel login
   ```

3. **Deploy to Preview**:
   ```bash
   vercel
   ```

4. **Deploy to Production**:
   ```bash
   vercel --prod
   ```

### Option 2: Deploy via Vercel Dashboard

1. Go to [vercel.com/new](https://vercel.com/new)
2. Import your Git repository
3. Select the `Agents` branch
4. Add environment variables:
   - `HF_TOKEN` (required)
   - `HF_MODEL_ID` (optional, defaults to "AdaptLLM/law-LLM")
5. Click "Deploy"

## Environment Variables Setup

Set these in Vercel Dashboard → Settings → Environment Variables:

```bash
HF_TOKEN=your_huggingface_token_here
HF_MODEL_ID=AdaptLLM/law-LLM  # Optional
```

Or via CLI:
```bash
vercel env add HF_TOKEN
vercel env add HF_MODEL_ID
```

## Post-Deployment

After deployment, your app will be available at:
- **Preview**: `https://your-project-*.vercel.app`
- **Production**: `https://your-project.vercel.app`

Test the deployment:
1. Visit the homepage
2. Test the chat functionality
3. Check API endpoint: `https://your-project.vercel.app/api/legal-advice`

## Troubleshooting

If deployment fails:
1. Check build logs in Vercel Dashboard
2. Verify all environment variables are set
3. Ensure `pnpm` is available (Vercel auto-detects)
4. Check `api/requirements.txt` has all dependencies

## Files Changed for Vercel

- ✅ `vercel.json` - Updated configuration
- ✅ `api/index.py` - Added Mangum handler
- ✅ `api/requirements.txt` - Added Mangum dependency
- ✅ `fastapi_server/requirements.txt` - Added Mangum
- ✅ `client/pages/Chat.tsx` - Updated API URL for production
- ✅ `.vercelignore` - Added ignore patterns

