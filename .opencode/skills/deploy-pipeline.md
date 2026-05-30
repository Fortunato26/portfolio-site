# Skill: Deploy Pipeline

## Description
Sets up deployment pipelines for web applications using Vercel, Netlify, GitHub Actions, and other platforms.

## When to Use
- Deploying first project
- Setting up CI/CD
- Configuring custom domains
- Automating deployments

## Instructions

### Vercel (Recommended for Next.js)

#### First Deploy
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Deploy to production
vercel --prod
```

#### Automatic Deploy
- Connect GitHub repository
- Every push to `main` triggers deploy
- PR previews generated automatically

#### Custom Domain
```bash
# Add domain
vercel domains add yourdomain.com

# Or in dashboard:
# Settings > Domains > Add
```

### Netlify (Recommended for Static)

#### Manual Deploy
```bash
# Install Netlify CLI
npm i -g netlify-cli

# Deploy
netlify deploy --prod
```

#### netlify.toml
```toml
[build]
  command = "npm run build"
  publish = "dist"

[build.environment]
  NODE_VERSION = "18"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

### GitHub Actions

#### Basic Workflow
```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: 18
          
      - name: Install dependencies
        run: npm ci
        
      - name: Run tests
        run: npm test
        
      - name: Build
        run: npm run build
        
      - name: Deploy to Vercel
        uses: amondnet/vercel-action@v20
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: ${{ secrets.VERCEL_ORG_ID }}
          vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID }}
          vercel-args: '--prod'
```

### Environment Variables

#### Vercel
```bash
# Add via CLI
vercel env add NEXT_PUBLIC_API_URL

# Or in dashboard:
# Settings > Environment Variables
```

#### GitHub Secrets
```
Settings > Secrets and variables > Actions > New repository secret

Name: VERCEL_TOKEN
Value: your_token_here
```

### Custom Domain Setup

#### DNS Configuration
```
Type    Name    Value
A       @       76.76.21.21
CNAME   www     cname.vercel-dns.com
```

#### SSL Certificate
- Vercel/Netlify provide free SSL automatically
- No configuration needed

### Deploy Checklist
- [ ] Build succeeds locally
- [ ] Tests pass
- [ ] No console errors
- [ ] Environment variables set
- [ ] Custom domain configured
- [ ] SSL enabled
- [ ] 404 page configured
- [ ] Analytics enabled (optional)

## References
- [[Next.js - Referência Completa]]
- [[Node.js - Referência Completa]]
