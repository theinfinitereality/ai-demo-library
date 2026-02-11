# Security Guidelines

This document outlines the security measures implemented in the AI Demo Library project.

## 🔒 Security Features

### 1. Nginx Security Headers

The following security headers are configured in `nginx.conf`:

- **X-Frame-Options**: `SAMEORIGIN` - Prevents clickjacking attacks
- **X-Content-Type-Options**: `nosniff` - Prevents MIME type sniffing
- **X-XSS-Protection**: `1; mode=block` - Enables XSS filtering
- **Referrer-Policy**: `strict-origin-when-cross-origin` - Controls referrer information
- **Permissions-Policy**: Restricts access to browser features (geolocation, microphone, camera)
- **Content-Security-Policy**: Restricts resource loading to trusted sources
- **Server Tokens**: Hidden to prevent version disclosure

### 2. Service Account Security

The GitHub Actions service account (`github-actions@genai-analytics-435321.iam.gserviceaccount.com`) should have **minimal permissions**:

**Required Roles:**
- `roles/run.admin` - Deploy to Cloud Run
- `roles/storage.admin` - Push to Google Container Registry
- `roles/iam.serviceAccountUser` - Act as service account

**Note**: The current service account may have additional permissions from previous projects. For production, consider creating a dedicated service account with only the required roles.

### 3. Secrets Management

**GitHub Secrets** (stored in repository settings):
- `GCP_PROJECT_ID` - Google Cloud Project ID
- `GCP_SA_KEY` - Service account JSON key (encrypted by GitHub)

**Never commit:**
- Service account keys (`*.json` files)
- Environment variables (`.env` files)
- API keys or tokens
- Private keys

### 4. File Security

The `.gitignore` file prevents committing:
- Service account keys (`*.json`)
- Environment files (`.env*`)
- Reference materials (`reference/`)
- System files (`.DS_Store`, etc.)

### 5. Container Security

**Dockerfile best practices:**
- Uses official `nginx:alpine` base image (minimal attack surface)
- Runs as non-root user (nginx default)
- Only copies necessary files
- No secrets in image layers

### 6. Cloud Run Security

**Deployment configuration:**
- Unauthenticated access allowed (public demo site)
- Automatic HTTPS enforcement by Cloud Run
- Automatic DDoS protection
- Regional deployment for compliance

## 🔐 Security Checklist

Before deploying:

- [ ] Service account key is not committed to repository
- [ ] GitHub secrets are properly configured
- [ ] Nginx security headers are enabled
- [ ] No sensitive data in Docker image
- [ ] `.gitignore` includes all sensitive files
- [ ] Service account has minimal required permissions
- [ ] HTTPS is enforced (automatic with Cloud Run)
- [ ] Dependencies are up to date

## 🚨 Security Incident Response

If a security issue is discovered:

1. **Do not** create a public GitHub issue
2. Rotate compromised credentials immediately
3. Contact the security team
4. Review access logs
5. Update this document with lessons learned

## 📝 Audit Log

- **2024-02-11**: Initial security configuration
  - Added security headers to nginx
  - Configured service account with required permissions
  - Set up GitHub secrets for deployment
  - Created `.gitignore` for sensitive files

## 🔄 Regular Security Tasks

- [ ] Review service account permissions quarterly
- [ ] Rotate service account keys annually
- [ ] Update base Docker image monthly
- [ ] Review nginx security headers quarterly
- [ ] Audit GitHub Actions logs monthly

## 📚 References

- [OWASP Security Headers](https://owasp.org/www-project-secure-headers/)
- [Google Cloud IAM Best Practices](https://cloud.google.com/iam/docs/best-practices)
- [GitHub Actions Security](https://docs.github.com/en/actions/security-guides)
- [Nginx Security](https://nginx.org/en/docs/http/ngx_http_ssl_module.html)

