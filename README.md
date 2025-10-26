# Myndy AI SMS - Android SMS Gateway

Myndy AI SMS is an open-source SMS gateway that enables users to send and receive SMS messages via a web dashboard or a REST API. Perfect for businesses, developers, and hobbyists who need a reliable and cost-effective way to automate SMS messaging.

- **Technology stack**: React, Next.js, Node.js, NestJS, MongoDB, Android, Java
- **Part of the Myndy AI ecosystem** - integrated with Myndy AI's personal assistant platform


## Features

- Send & receive SMS messages via API & dashboard
- Use your own Android phone as an SMS gateway
- REST API for easy integration with apps & services
- Send Bulk SMS with CSV file
- Multi-device support for higher SMS throughput
- Secure API authentication with API keys
- Webhook support
- Self-hosting support for full control over your data




## Getting Started

1. Set up your Myndy AI SMS instance (see Self-Hosting section below)
2. Install the app on your Android phone
3. Open the app and grant the permissions for SMS
4. Go to your dashboard and click register device / generate API Key
5. Scan the QR code with the app or enter the API key manually
6. You are ready to send SMS messages from the dashboard or from your application via the REST API

**Code Snippet**: Few lines of code showing how to send an SMS message via the REST API

```javascript
const API_KEY = 'YOUR_API_KEY';
const DEVICE_ID = 'YOUR_DEVICE_ID';
const API_BASE_URL = 'YOUR_API_BASE_URL'; // e.g., http://localhost:3001

await axios.post(`${API_BASE_URL}/api/v1/gateway/devices/${DEVICE_ID}/send-sms`, {
  recipients: [ '+251912345678' ],
  message: 'Hello World!',
}, {
  headers: {
    'x-api-key': API_KEY,
  },
});

```

**Code Snippet**: Curl command to send an SMS message via the REST API

```bash
curl -X POST "YOUR_API_BASE_URL/api/v1/gateway/devices/YOUR_DEVICE_ID/send-sms" \
  -H 'x-api-key: YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "recipients": [ "+251912345678" ],
    "message": "Hello World!"
  }'
```

### Receiving SMS Messages

To receive SMS messages, you can enable the feature from the mobile app. You can then fetch the received SMS messages via the REST API or view them in the dashboard.

**Code Snippet**: Few lines of code showing how to fetch received SMS messages via the REST API

```javascript
const API_KEY = 'YOUR_API_KEY';
const DEVICE_ID = 'YOUR_DEVICE_ID';
const API_BASE_URL = 'YOUR_API_BASE_URL';

await axios.get(`${API_BASE_URL}/api/v1/gateway/devices/${DEVICE_ID}/get-received-sms`, {
  headers: {
    'x-api-key': API_KEY,
  },
});

```

**Code Snippet**: Curl command to fetch received SMS messages

```bash
curl -X GET "YOUR_API_BASE_URL/api/v1/gateway/devices/YOUR_DEVICE_ID/get-received-sms"\
  -H "x-api-key: YOUR_API_KEY"
```

## Self-Hosting

### Setting Up Database

1. **Install MongoDB on Your Server**: Follow the official MongoDB installation guide for your operating system.
2. **Using MongoDB Atlas**: Alternatively, you can create a free database on MongoDB Atlas. Sign up at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) and follow the instructions to set up your database.

### Firebase Setup

1. Create a Firebase project.
2. Enable Firebase Cloud Messaging (FCM) in your Firebase project.
3. Obtain the Firebase credentials for backend use and the Android app.

### Building the Android App

1. Clone the repository and navigate to the Android project directory.
2. Update the `google-services.json` file with your Firebase project configuration.
3. Update the API base URL configuration in the project.
4. Build the app using Android Studio or the command line:
   ```bash
   ./gradlew assembleRelease
   ```

### Building the Web

1. Navigate to the `web` directory.
2. Copy the `.env.example` file to `.env`:
   ```bash
   cp .env.example .env
   ```
3. Update the `.env` file with your own credentials.
4. Install dependencies:
   ```bash
   pnpm install
   ```
5. Build the web application:
   ```bash
   pnpm build
   ```

### Building the API

1. Navigate to the `api` directory.
2. Copy the `.env.example` file to `.env`:
   ```bash
   cp .env.example .env
   ```
3. Update the `.env` file with your own credentials.
4. Install dependencies:
   ```bash
   pnpm install
   ```
5. Build the API:
   ```bash
   pnpm build
   ```

### Hosting on a VPS

1. Install `pnpm`, `pm2`, and `Caddy` (or nginx) on your VPS.
2. Use `pm2` to manage your Node.js processes:
   ```bash
   pm2 start dist/main.js --name myndy-sms-api
   ```
3. Configure `Caddy` to serve your web application and API. Example Caddyfile:
   ```
   your-domain.com {
       reverse_proxy /api/* localhost:3001
       reverse_proxy /* localhost:3000
   }
   ```
4. Ensure your domain points to your VPS and Caddy is configured properly.

### Dockerized Environment
#### Requirements:
- Docker installed

1. After setting up Firebase, update your `.env` in `web` && `api` folder.
   ```bash
   cd web && cp .env.example .env \
   && cd ../api && cp .env.example .env
   ```
2. Navigate to root folder and execute docker-compose.yaml file.
   This will spin up `web` container, `api` container alongside with `MongoDB` and `MongoExpress`. `myndy_sms` database will be automatically created.
   ```bash
   docker compose up -d
   ```
   To stop the containers simply type
   ```bash
   docker compose down
   ```

## Contributing

Contributions are welcome!

1. Fork the project.
2. Create a feature or bugfix branch from `main` branch.
3. Make sure your commit messages and PR comment summaries are descriptive.
4. Create a pull request to the `main` branch.

## Bug Reporting and Feature Requests

Please feel free to create an issue in the repository for any bug reports or feature requests. Make sure to provide a detailed description of the issue or feature you are requesting and properly label whether it is a bug or a feature request.

Please note that if you discover any vulnerability or security issue, we kindly request that you refrain from creating a public issue. Instead, report it through appropriate security channels.

## Support

For support, feedback, and questions, please reach out through the Myndy AI channels or create an issue in this repository.
