# CryptoFD - Production Deployment Guide

## System Architecture

- **Frontend:** Next.js 16 (React 19, TypeScript)
- **Backend:** Next.js API Routes + Prisma ORM
- **Database:** PostgreSQL (Render)
- **Authentication:** JWT + Email OTP
- **Crypto:** ethers.js for blockchain integration
- **Email:** Resend API

## Production Deployment Checklist

### ✅ Environment Setup
- [ ] Database URL configured in Render
- [ ] All environment variables set (see .env.example)
- [ ] JWT_SECRET generated and configured
- [ ] Resend API key added for email service
- [ ] NEXT_PUBLIC_APP_URL set to production domain

### ✅ Security
- [ ] Password hashing enabled (bcryptjs)
- [ ] JWT tokens with 24-hour expiration
- [ ] Email OTP verification for new accounts
- [ ] CORS properly configured
- [ ] Input validation on all API endpoints
- [ ] SQL injection prevention via Prisma

### ✅ Performance
- [ ] Next.js build optimized
- [ ] Database indexes created
- [ ] Caching headers configured
- [ ] Image optimization enabled
- [ ] Static pages pre-rendered where possible

### ✅ Monitoring
- [ ] Health check endpoint: `/api/health`
- [ ] Error logging configured
- [ ] Database connection monitoring
- [ ] Render auto-scaling enabled
- [ ] Uptime monitoring enabled

## Deployment Steps

### Local Development
```bash
# Install dependencies
pnpm install

# Setup environment
cp .env.example .env.local

# Run database migrations
pnpm prisma db push

# Start dev server
pnpm dev
```

### Render Deployment
```
1. Connect GitHub repository
2. Set environment variables in Render dashboard
3. Configure build command: pnpm install && pnpm prisma db push && pnpm build
4. Configure start command: pnpm start
5. Deploy automatically on push to main
```

## Health Check

Test deployment health:
```bash
curl https://yourdomain.com/api/health
```

Expected response:
```json
{
  "status": "healthy",
  "timestamp": "2024-06-03T12:00:00Z",
  "uptime": 3600,
  "environment": "production"
}
```

## Database Schema

Run Prisma Studio to view/edit data:
```bash
pnpm prisma studio
```

## Production Features

- User authentication with email verification
- Trading analytics dashboard
- Fixed Deposit (FD) management
- Referral program
- Admin trading data management
- Real-time chat support
- Dark mode theme
- Responsive design

## Support

For deployment issues, check Render logs:
https://dashboard.render.com → cryptofd → Logs
