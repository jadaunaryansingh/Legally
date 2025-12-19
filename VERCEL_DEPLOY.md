# Vercel Deployment Guide

## Prerequisites

1. **Vercel Account**: Sign up at [vercel.com](https://vercel.com)
2. **Vercel CLI** (optional, for CLI deployment):
   ```bash
   npm i -g vercel
   ```

## Environment Variables

Before deploying, set these environment variables in Vercel Dashboard:

1. **HF_TOKEN** - Your Hugging Face API token
2. **HF_MODEL_ID** (optional) - Defaults to "AdaptLLM/law-LLM"
3. **VITE_LEGAL_API_URL** (optional) - Leave empty for production (uses relative URL)

### Setting Environment Variables in Vercel:

1. Go to your project in Vercel Dashboard
2. Navigate to **Settings** → **Environment Variables**
3. Add each variable for **Production**, **Preview**, and **Development** environments

## Deployment Methods

### Method 1: Deploy via Vercel Dashboard (Recommended)

1. **Push your code to GitHub/GitLab/Bitbucket**
   ```bash
   git add .
   git commit -m "Prepare for Vercel deployment"
   git push origin Agents  # or your branch name
   ```

2. **Import Project in Vercel**:
   - Go to [vercel.com/new](https://vercel.com/new)
   - Import your Git repository
   - Vercel will auto-detect the configuration from `vercel.json`

3. **Configure Environment Variables** (see above)

4. **Deploy**: Click "Deploy" and wait for build to complete

### Method 2: Deploy via Vercel CLI

1. **Install Vercel CLI** (if not already installed):
   ```bash
   npm i -g vercel
   ```

2. **Login to Vercel**:
   ```bash
   vercel login
   ```

3. **Deploy**:
   ```bash
   vercel
   ```
   
   For production deployment:
   ```bash
   vercel --prod
   ```

4. **Set Environment Variables via CLI**:
   ```bash
   vercel env add HF_TOKEN
   vercel env add HF_MODEL_ID
   ```

## Project Configuration

The project is configured via `vercel.json`:

- **Build Command**: `pnpm run build:client`
- **Output Directory**: `dist/spa`
- **Python Runtime**: `python3.11` for API functions
- **API Routes**: `/api/*` routes are handled by FastAPI serverless function

## Important Notes

1. **Branch**: Currently on `Agents` branch. Make sure to deploy from the correct branch.

2. **API Endpoints**: 
   - Frontend calls `/api/legal-advice` which is handled by the FastAPI serverless function
   - The function is located at `api/index.py`

3. **Build Process**:
   - Vercel will run `pnpm install --frozen-lockfile`
   - Then `pnpm run build:client` to build the React SPA
   - Python dependencies are installed from `api/requirements.txt`

4. **SPA Routing**: All non-API routes are rewritten to `/index.html` for React Router to handle

## Troubleshooting

### Build Fails

- Check that `pnpm` is available (Vercel should auto-detect)
- Verify `package.json` has correct build scripts
- Check build logs in Vercel Dashboard

### API Not Working

- Verify `HF_TOKEN` environment variable is set
- Check `api/requirements.txt` includes all dependencies
- Review function logs in Vercel Dashboard → Functions tab

### Routing Issues

- Ensure `vercel.json` has correct rewrite rules
- Check that React Router is configured for SPA mode

## Post-Deployment

After successful deployment:

1. **Test the API**: Visit `https://your-project.vercel.app/api/legal-advice` (should return FastAPI docs or error)
2. **Test Frontend**: Visit `https://your-project.vercel.app` and test the chat functionality
3. **Monitor**: Check Vercel Dashboard for function logs and analytics

## Custom Domain

To add a custom domain:

1. Go to **Settings** → **Domains** in Vercel Dashboard
2. Add your domain
3. Follow DNS configuration instructions

