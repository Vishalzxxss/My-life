# Deploying TrackDown to Vercel

This guide provides step-by-step instructions for deploying TrackDown to Vercel's serverless platform.

## Prerequisites

1. A Telegram Bot Token (create one using [@BotFather](https://t.me/BotFather))
2. A Vercel account ([sign up here](https://vercel.com/signup))
3. Git installed on your local machine

## Deployment Steps

### 1. Prepare your Environment Variables

Create a `.env` file based on the provided `.env.sample`:

```bash
cp .env.sample .env
```

Edit the `.env` file and add your Telegram Bot Token:

```
BOT_TOKEN=1234567890:ABCDEFGHIJKLMNOPQRSTUVWXYZ
```

The other variables will be configured after deployment.

### 2. Deploy to Vercel

#### Option A: Using the Vercel CLI

Install Vercel CLI:

```bash
npm i -g vercel
```

Deploy the application:

```bash
vercel
```

Follow the prompts to link to your Vercel account and project.

#### Option B: Using the Vercel Dashboard

1. Push your code to a GitHub repository
2. Go to [Vercel Dashboard](https://vercel.com/dashboard)
3. Click "New Project"
4. Import your GitHub repository
5. Configure the project settings
6. Deploy

### 3. Configure Environment Variables on Vercel

1. Go to your Vercel dashboard
2. Select your deployed project
3. Navigate to "Settings" > "Environment Variables"
4. Add all the variables from your `.env` file
5. Update the following variables with your actual Vercel deployment URL:
   - `HOST_URL` = `https://your-vercel-url.vercel.app`
   - `WEBHOOK_URL` = `https://your-vercel-url.vercel.app/webhook`

### 4. Set Up Telegram Bot Webhook

After deploying and configuring environment variables, set the webhook for your Telegram Bot:

```
https://api.telegram.org/bot<YOUR_BOT_TOKEN>/setWebhook?url=<YOUR_VERCEL_URL>/webhook
```

Replace `<YOUR_BOT_TOKEN>` with your actual bot token and `<YOUR_VERCEL_URL>` with your Vercel deployment URL.

## Vercel Free Tier Limitations

TrackDown is optimized to work within Vercel's free tier limits:

- **Execution Time**: 10 seconds maximum per function
- **Memory**: 1024MB per function
- **Storage**: No persistent storage (files in `/tmp` are temporary)
- **Concurrency**: Limited in free tier

For heavy media processing or high-traffic usage, consider upgrading to Vercel's Pro plan.

## Troubleshooting

### Webhook Issues

If your bot isn't responding to messages, verify that:

1. The webhook is properly set (use the command in step 4)
2. The Telegram Bot Token is correctly set in environment variables
3. The `HOST_URL` and `WEBHOOK_URL` are correct

### Media Processing Issues

If media (photos, videos) isn't being processed correctly:

1. Check that your deployment is within Vercel's free tier limits
2. Media files that are too large may time out during processing
3. Use the application logs in Vercel dashboard to identify specific errors