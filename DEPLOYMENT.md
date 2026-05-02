# 🚀 Deployment Guide

Deploy your Vibe Codes AI Images app to production using various platforms.

## Option 1: Vercel (Recommended for Frontend)

### Frontend Deployment

1. **Push to GitHub**: Ensure code is in your repository

2. **Connect to Vercel**:
   - Go to https://vercel.com
   - Click "Import Project"
   - Select your `Vibe-Codes-AI-Images` repository
   - Choose "Next.js" preset

3. **Configure**:
   - Set build command: `cd client && npm run build`
   - Set output directory: `client/dist`

4. **Environment Variables**:
   - Add `VITE_API_URL=https://your-backend-url.com`

5. **Deploy**: Click "Deploy"

Your frontend will be live! 🎉

## Option 2: Render (Free Backend Hosting)

### Backend Deployment

1. **Prepare for Deployment**:

Create `server/Procfile`:
```
web: node index.js
```

2. **Push to GitHub**

3. **Connect to Render**:
   - Go to https://render.com
   - Click "New +" → "Web Service"
   - Connect your GitHub repository
   - Select the repository

4. **Configure**:
   - **Name**: `vibe-codes-ai-backend`
   - **Environment**: `Node`
   - **Build Command**: `npm install && cd server && npm install`
   - **Start Command**: `cd server && npm start`
   - **Region**: Select closest to you

5. **Set Environment Variables**:
   - Click "Environment"
   - Add:
     ```
     OPENAI_API_KEY=your_key_here
     NODE_ENV=production
     CLIENT_URL=https://your-vercel-app.vercel.app
     ```

6. **Deploy**: Click "Create Web Service"

Get your backend URL (e.g., `https://vibe-codes-ai-backend.onrender.com`)

## Option 3: Heroku (Paid, Deprecated Free Tier)

### Backend on Heroku

```bash
# Install Heroku CLI
npm install -g heroku

# Login
heroku login

# Create app
heroku create vibe-codes-ai-backend

# Set environment variables
heroku config:set OPENAI_API_KEY=your_key_here
heroku config:set NODE_ENV=production
heroku config:set CLIENT_URL=https://your-frontend.vercel.app

# Deploy
git push heroku main
```

## Option 4: AWS (Production Grade)

### Backend on AWS EC2

1. **Create EC2 Instance**:
   - Use Ubuntu 22.04 LTS
   - Allow ports 22 (SSH), 80 (HTTP), 443 (HTTPS)

2. **SSH into Instance**:
```bash
ssh -i your-key.pem ubuntu@your-instance-ip
```

3. **Install Dependencies**:
```bash
sudo apt update
sudo apt install nodejs npm
sudo apt install nginx

# Clone repository
git clone https://github.com/bats314159/Vibe-Codes-AI-Images.git
cd Vibe-Codes-AI-Images
npm install
cd server && npm install && cd ..
```

4. **Configure Environment**:
```bash
nano server/.env
# Add your configuration
```

5. **Install PM2** (Process Manager):
```bash
sudo npm install -g pm2
cd server
pm2 start index.js --name "vibe-codes-api"
pm2 startup
pm2 save
```

6. **Configure Nginx** (Reverse Proxy):
```bash
sudo nano /etc/nginx/sites-available/default
```

Add:
```nginx
server {
    listen 80 default_server;
    server_name your-domain.com;

    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

7. **Enable SSL** (with Let's Encrypt):
```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d your-domain.com
```

## Option 5: Railway.app

### Full Stack Deployment

1. Go to https://railway.app
2. Click "Create New Project"
3. Select "Deploy from GitHub"
4. Choose your repository
5. Add services:
   - **Ensure `NODE_ENV=production`**
   - **Set `OPENAI_API_KEY`**
   - **Set `CLIENT_URL`**
6. Railway automatically detects `package.json` and deploys

## Option 6: Replit

### Quick Deployment

1. Go to https://replit.com
2. Click "New Repl" → "Import from GitHub"
3. Paste your repository URL
4. Add `.env` file with credentials
5. Run `npm run dev`

Share the Replit link publicly (limited to free tier resources)

## 🔒 Security Best Practices

### Before Going Live

1. **Rotate API Keys**:
   - Generate a new OpenAI API key
   - Delete the old one from platform.openai.com

2. **Enable HTTPS**:
   - Use Let's Encrypt (free SSL/TLS)
   - All platforms above support HTTPS

3. **Environment Variables**:
   - Never commit `.env` to Git
   - Use platform's secret management

4. **Rate Limiting**:
   - Add rate limiting to your API
   - Prevent abuse of your OpenAI quota

Example rate limiting in `server/index.js`:
```javascript
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
  windowMs: 60 * 1000, // 1 minute
  max: 5 // 5 requests per minute
});

app.post('/api/generate', limiter, generateImage);
```

5. **CORS Configuration**:
```javascript
app.use(cors({
  origin: process.env.CLIENT_URL,
  credentials: true
}));
```

## 📊 Monitoring

### Set Up Error Tracking

Use Sentry:

1. Create account at https://sentry.io
2. Install in server:
```bash
npm install @sentry/node
```

3. Add to `server/index.js`:
```javascript
const Sentry = require("@sentry/node");

Sentry.init({ dsn: process.env.SENTRY_DSN });
```

### Monitor API Usage

- Check https://platform.openai.com/account/billing/overview regularly
- Set up billing alerts in OpenAI dashboard

## 🔧 Post-Deployment

1. **Update Frontend URL**: Update API calls to point to production backend
2. **Test**: Verify image generation works end-to-end
3. **Monitor**: Check logs and error tracking
4. **Optimize**: Monitor performance and adjust as needed

## 💰 Cost Estimate (Monthly)

- **DALL-E 3**: $0.040 - $0.080 per image
- **Vercel Frontend**: $0 - $20/month
- **Render Backend**: $7/month (or free with cold starts)
- **Domain**: $10-15/year
- **Total**: Depends on image volume

## 🆘 Troubleshooting Deployment

### Cold Start Issues on Render/Railway
- First request takes 30-60 seconds
- Solution: Use `@app.get('/health')` endpoint for heartbeat

### CORS Errors After Deployment
- Verify `CLIENT_URL` matches your deployed frontend
- Check proxy settings in your framework

### API Key Not Working
- Verify key is correctly set in platform environment variables
- Not escaped or truncated

### High Memory Usage
- Implement image cleanup in database
- Use CDN for image delivery

## 📚 Additional Resources

- [Vercel Docs](https://vercel.com/docs)
- [Render Docs](https://render.com/docs)
- [AWS EC2 Guide](https://docs.aws.amazon.com/ec2/)
- [OpenAI API Reference](https://platform.openai.com/docs/api-reference)

Happy deploying! 🚀
