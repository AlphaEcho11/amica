# Amica Deployment Guide

This guide provides instructions for setting up and running Amica locally. There are several ways to run Amica:

*   **Web Application Only (Development):** For frontend development without running the desktop shell.
*   **Desktop Application (Development):** Runs both the web server and the Electron app for integrated development.
*   **Web Application (Docker):** The recommended way to run the web application in a production-like environment.
*   **Desktop Application (Production Build):** To create a distributable desktop application.

---

## 1. Prerequisites

Before you begin, ensure you have the following software installed:

*   **Node.js:** Version `18.18.0` or newer. You can download it from the [official Node.js website](https://nodejs.org/).
*   **npm** or **yarn**: A package manager for Node.js.
*   **Git**: For cloning the repository.
*   **Rust**: Required for building the native modules used by the application. Install it using `rustup` from the [official Rust website](https://www.rust-lang.org/tools/install). The native modules are built automatically during `npm install`.
*   **Docker** (Optional): Required if you want to run the application with Docker. You can get it from the [Docker website](https://www.docker.com/get-started).


---

## 2. Initial Setup

#### Step 1: Clone the Repository

```bash
git clone https://github.com/semperai/amica.git
cd amica
```

#### Step 2: Install Dependencies

This command will install all necessary packages and build the Rust native modules.

```bash
npm install
```

#### Step 3: Configure the Application

Amica is configured using an `.env.local` file. You can create this file by copying the example file if one exists, or by creating a new file in the root of the project.

```bash
# cp .env.local.example .env.local
```

If `.env.local.example` does not exist, create `.env.local` and add the necessary environment variables. You can find a list of available options in `src/utils/config.ts`.


---

## 3. Running in Development Mode

### Web Application Only

If you only want to run the web interface (for example, for UI development), use this command:

```bash
npm run dev:next
```

The application will be available at [http://localhost:3000](http://localhost:3000).

### Desktop Application

To run the full desktop application in development mode, which includes the web server and the Electron app, use this command:

```bash
npm run dev
```

This will launch the Electron application, and changes to the code will trigger hot-reloading.

---

## 4. Building for Production

### Web Application (Docker)

This method uses Docker and Docker Compose to build and run the web application in a container.

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

### Desktop Application

To build the final, standalone executable for the desktop application, run the following command:

```bash
npm run build
```

This command bundles both the web application and the Electron shell. The build process will create an executable file in the `dist/` directory. The output will vary depending on your operating system (e.g., a `.exe` installer on Windows, a `.dmg` on macOS, or an `.AppImage` on Linux).
