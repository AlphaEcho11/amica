# Amica Deployment Guide

This guide provides instructions for setting up and running Amica locally. There are three main ways to run Amica:

1.  **Run the web application in development mode:** The quickest way to get started and see your changes.
2.  **Run the web application with Docker:** The recommended way to run the application in a production-like environment.
3.  **Run the desktop application:** For running Amica as a standalone desktop app.

---

## 1. Prerequisites

Before you begin, ensure you have the following software installed:

*   **Node.js:** Version `18.18.0` or newer. You can download it from the [official Node.js website](https://nodejs.org/).
*   **npm** or **yarn**: A package manager for Node.js.
*   **Git**: For cloning the repository.
*   **Docker** (Optional): Required for running the application with Docker. You can get it from the [Docker website](https://www.docker.com/get-started).
*   **Rust** (Optional): Required for building the desktop application. Install it using `rustup` from the [official Rust website](https://www.rust-lang.org/tools/install).

---

## 2. Configuration

Amica is configured using an `.env.local` file. You can create this file by copying the example file if one exists, or by creating a new file in the root of the project.

```bash
cp .env.local.example .env.local
```

If `.env.local.example` does not exist, create `.env.local` and add the necessary environment variables. You can find a list of available options in `src/utils/config.ts`.

---

## 3. Running the Web Application (Development Mode)

This method is ideal for development and testing.

#### Step 1: Clone the Repository

```bash
git clone https://github.com/semperai/amica.git
cd amica
```

#### Step 2: Install Dependencies

```bash
npm install
```

#### Step 3: Run the Development Server

```bash
npm run dev
```

The application will be available at [http://localhost:3000](http://localhost:3000).

---

## 4. Building and Running with Docker

This method uses Docker and Docker Compose to build and run the application in a container. This is the recommended way to run the application in a production-like environment.

#### Step 1: Build and Run the Container

```bash
docker-compose up --build
```

The application will be available at [http://localhost:80](http://localhost:80).

To run the container in the background, use the `-d` flag:

```bash
docker-compose up --build -d
```

To stop the container, run:

```bash
docker-compose down
```

---

## 5. Building the Desktop Application

Amica can be run as a standalone desktop application using Tauri.

#### Step 1: Install Desktop-Specific Dependencies

On Linux, you may need to install additional packages:

```bash
sudo apt-get update
sudo apt-get install -y libwebkit2gtk-4.0-dev build-essential curl wget libssl-dev libgtk-3-dev libayatana-appindicator3-dev librsvg2-dev
```

#### Step 2: Run the Application in Development Mode

This command will build and launch the desktop application in a development window with hot-reloading.

```bash
npm run tauri dev
```

#### Step 3: Build the Application for Production

To build the final, standalone executable, run the following command:

```bash
npm run tauri build
```

The build process will create an executable file in the `src-tauri/target/release/bundle/` directory. The output will vary depending on your operating system (e.g., `.msi` on Windows, `.app` and `.dmg` on macOS, `.AppImage` and `.deb` on Linux).
