# Deploy Viewpoint Manager to Fly.io

## Prerequisites

1. Install Fly.io CLI:
   ```bash
   # macOS
   brew install flyctl
   
   # Linux
   curl -L https://fly.io/install.sh | sh
   
   # Windows
   powershell -Command "iwr https://fly.io/install.ps1 -useb | iex"
   ```

2. Sign up or login to Fly.io:
   ```bash
   flyctl auth signup
   # or
   flyctl auth login
   ```

## Deployment Steps

### 1. Navigate to the project directory
```bash
cd /path/to/viewpoint-manager
```

### 2. Launch the app
```bash
flyctl launch
```

When prompted:
- **App name**: Press Enter to use "viewpoint-manager" or choose your own
- **Organization**: Choose your organization
- **Region**: Choose closest to you (default: sjc - San Jose, CA)
- **Would you like to set up a Postgresql database?**: No
- **Would you like to set up an Upstash Redis database?**: No
- **Would you like to deploy now?**: Yes

### 3. Wait for deployment
Fly.io will:
- Build your Docker image
- Deploy to their infrastructure
- Provide you with a URL like: `https://viewpoint-manager.fly.dev`

### 4. Open your app
```bash
flyctl open
```

## Managing Your App

### View logs
```bash
flyctl logs
```

### Check status
```bash
flyctl status
```

### Deploy updates
After making changes:
```bash
flyctl deploy
```

### Scale (if needed)
```bash
# Add more memory
flyctl scale memory 512

# Add more machines
flyctl scale count 2
```

### Delete the app
```bash
flyctl apps destroy viewpoint-manager
```

## Troubleshooting

### Build fails
- Make sure all files are in the correct structure
- Check that Docker is working: `docker --version`

### App won't start
- Check logs: `flyctl logs`
- Verify port 3000 is exposed in Dockerfile

### Out of memory
- Increase memory: `flyctl scale memory 512`

## Cost

Fly.io offers:
- **Free tier**: 3 shared-cpu VMs with 256MB RAM
- Your app should fit in the free tier with these settings

## Project Structure

```
viewpoint-manager/
├── public/
│   └── index.html
├── src/
│   ├── App.js
│   └── index.js
├── Dockerfile
├── fly.toml
├── package.json
├── .dockerignore
└── DEPLOY.md (this file)
```

## Notes

- The app uses browser localStorage for data persistence
- No backend database is needed
- All data is stored client-side
- Each user has their own isolated data

## Support

- Fly.io Docs: https://fly.io/docs/
- Fly.io Community: https://community.fly.io/
