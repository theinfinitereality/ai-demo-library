# Napster.ai - AI Demo Library

A showcase of cutting-edge AI demonstrations powered by Napster.ai technology.

## 🚀 Live Demos

Visit our demo library to explore:

- **AI Interviewer** - Intelligent interview simulations
- **AI Pitch Deck** - AI-powered presentation generation
- **AI Retail Demo - Nissan** - Automotive retail experiences
- **Google Home AI Deck** - Smart home presentations
- **Google Nest Products Demo** - Connected living demonstrations
- **KACST Web UI** - Research platform integration

## 🛠️ Technology Stack

- **Frontend**: HTML5, CSS3, Vanilla JavaScript
- **Web Server**: Nginx (Alpine)
- **Container**: Docker
- **Hosting**: Google Cloud Run
- **CI/CD**: GitHub Actions

## 📦 Deployment

This project uses automated deployment to Google Cloud Run via GitHub Actions.

### Prerequisites

1. Google Cloud Project with billing enabled
2. Service account with Cloud Run Admin and Storage Admin roles
3. GitHub repository secrets configured

### Required GitHub Secrets

Add these secrets to your GitHub repository (Settings → Secrets and variables → Actions):

- `GCP_PROJECT_ID` - Your Google Cloud Project ID
- `GCP_SA_KEY` - Service account JSON key with deployment permissions

### Automatic Deployment

Every push to the `main` branch triggers automatic deployment:

1. Builds Docker image
2. Pushes to Google Container Registry
3. Deploys to Cloud Run
4. Outputs the service URL

### Manual Deployment

```bash
# Build Docker image
docker build -t ai-demo-library .

# Run locally
docker run -p 8080:8080 ai-demo-library

# Visit http://localhost:8080
```

## 🏗️ Project Structure

```
ai-demo-library/
├── index.html              # Main page
├── styles.css              # Styling
├── assets/                 # Images and logos
│   ├── logo.svg           # Napster.ai logo
│   └── *.png              # Demo screenshots
├── Dockerfile             # Container configuration
├── nginx.conf             # Web server configuration
└── .github/
    └── workflows/
        └── deploy.yml     # CI/CD pipeline
```

## 🔧 Local Development

Simply open `index.html` in your browser or use a local server:

```bash
# Using Python
python -m http.server 8080

# Using Node.js
npx serve -p 8080
```

## 📝 License

© 2024 Napster.ai - All rights reserved

## 🤝 Contributing

This is a showcase project for Napster.ai demonstrations.

