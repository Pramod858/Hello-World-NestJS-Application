# Hello World NestJS Application

This repository contains a simple "Hello World" application built using NestJS. The application can be automatically deployed to an AWS EC2 instance using GitHub Actions.

## Requirements

Before you begin, ensure you have met the following requirements:

- **Node.js**: Install Node.js (which includes npm). You can download it from [Node.js official website](https://nodejs.org/).
- **NestJS CLI**: Install the NestJS CLI globally using npm:
  ```bash
  npm install -g @nestjs/cli
  ```
- **AWS EC2 Instance**: An AWS EC2 instance to deploy the application. Ensure you have:
  - Public IP address of the instance.
  - SSH key pair for accessing the instance.

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/Pramod858/Hello-World-NestJS-Application.git
   cd Hello-World-NestJS-Application
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

## Running the Application Locally

To run the application locally, use the following command:

```bash
npm run start
```

The application will start, and you can access it at `http://localhost:3000`.

## Accessing the Hello World Endpoint

Open your browser and navigate to `http://localhost:3000/hello`. You should see the message "Hello World!".

## Deploying to AWS EC2 Using GitHub Actions

This repository is set up to use GitHub Actions for continuous deployment to an AWS EC2 instance. 

### Prerequisites

- Ensure your EC2 instance is running and accessible.
- Add the following secrets to your GitHub repository:
  - `AWS_EC2_KEY`: The content of your EC2 private key.
  - `AWS_EC2_HOST`: The public IP address of your EC2 instance.
  - `AWS_EC2_USER`: The username for your EC2 instance (e.g., `ubuntu`).

### GitHub Actions Workflow

The GitHub Actions workflow is defined in `.github/workflows/deploy.yml`. It is triggered on every push to the `main` branch and performs the following steps:

1. **Checkout the code** from the repository.
2. **Set up Node.js**.
3. **Install dependencies**.
4. **Deploy to EC2**:
   - Transfer the code to the EC2 instance using `rsync`.
   - SSH into the EC2 instance to install necessary packages and dependencies.
   - Build the application.
   - Use PM2 to manage the application process.

### Adding Secrets to GitHub

1. Go to your GitHub repository.
2. Navigate to `Settings` > `Secrets and variables` > `Actions`.
3. Click on `New repository secret`.
4. Add the following secrets:
   - `AWS_EC2_KEY`: Your EC2 private key content.
   - `AWS_EC2_HOST`: Your EC2 instance's public IP address.
   - `AWS_EC2_USER`: The username for your EC2 instance (e.g., `ubuntu`).

### Manual Deployment Steps (if needed)

1. **SSH into your EC2 instance**:
   ```bash
   ssh -i path/to/your-key.pem ubuntu@<your-ec2-ip>
   ```

2. **Install Node.js and npm**:
   ```bash
   sudo apt update
   sudo apt install -y nodejs npm
   ```

3. **Install NestJS CLI and PM2 globally**:
   ```bash
   sudo npm install -g @nestjs/cli pm2
   ```

4. **Clone the repository on the EC2 instance**:
   ```bash
   git clone https://github.com/Pramod858/Hello-World-NestJS-Application.git
   cd Hello-World-NestJS-Application
   ```

5. **Install dependencies**:
   ```bash
   npm install
   ```

6. **Build and start the application**:
   ```bash
   npm run build
   pm2 start dist/main.js --name nest-app
   ```

7. **Access your application**:
   Open your browser and navigate to `http://<your-ec2-ip>:3000`.

## Project Structure

Here's a quick overview of the project structure:

```
hello-world-nestjs/
├── src/
│   ├── app.controller.ts
│   ├── app.module.ts
│   ├── app.service.ts
│   └── hello/
│       └── hello.controller.ts
├── .github/
│   └── workflows/
│       └── deploy.yml
├── .gitignore
├── README.md
├── nest-cli.json
├── package.json
├── package-lock.json
├── tsconfig.build.json
└── tsconfig.json
```

## Contact

If you have any questions or feedback, feel free to contact me at [email](pramodbadiger45@gmail.com).
