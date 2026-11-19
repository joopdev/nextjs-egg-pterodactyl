# 🚀 Next.js Pterodactyl Egg

A custom, optimized Pterodactyl Egg for hosting Next.js applications.

This version resolves the common connectivity issue where Next.js servers show as "Ready" in the console but remain inaccessible via the browser/IP address due to incorrect network binding.

## 🧐 The Problem & Solution

By default, Next.js applications often bind to `localhost` (`127.0.0.1`). Inside a Docker container (which Pterodactyl uses), this prevents the application from being accessible from the outside world.

This Egg fixes that by automatically forcing the start command to listen on all interfaces (`0.0.0.0`), ensuring your site is immediately accessible after deployment.

It also improves startup reliability by using smarter dependency install behavior with package manager detection:
- **`auto` mode** detects lockfiles and picks `pnpm`, `yarn`, or `npm` automatically.
- **In `start` mode**, it installs all dependencies (including devDependencies such as Tailwind CSS, PostCSS and TypeScript) and builds before launch.
- **In `dev` mode**, it installs full dependencies so local development tools still work.

## 🧩 Supported Versions

This Egg comes pre-configured with all modern Node.js versions, selectable during installation:

- **Node.js 26 (Latest)**
- Node.js 25
- Node.js 24 (LTS)
- Node.js 23
- Node.js 22 (LTS)
- Node.js 21
- Node.js 20 (LTS)
- Node.js 19
- Node.js 18 (LTS)

✅ **Next.js Compatibility:** Supports all modern Next.js versions (13, 14, 15, 16+) that run on these Node environments.

## ✨ Features

- 🔌 **Instant Connectivity:** Pre-configured to listen on `0.0.0.0`, solving connection timeouts.
- 📦 **Auto-Install:** Clones your repository and installs dependencies on startup, using your lockfile.
- 🌱 **Ready on an Empty Server:** A new server without files gets a small starter page, so it starts right away.
- ⚙️ **Smart Build:** Runs `npm run build` automatically in production mode (`NODE_RUN_ENV=start`), with devDependencies installed so tools like Tailwind CSS and PostCSS work during the build.
- 🛡️ **Safe Next.js Updates:** On every start, Next.js is updated within your current version line (patch updates by default), so security fixes land automatically. Only Next.js is updated, the same way you would do it by hand (`npm install next@16.4.6`, `pnpm add`, `yarn add`). Your lockfile is kept and it never jumps to a new major version.
- 🔑 **Private Repositories:** Set the Git username and access token, and the server clones your private repository on first start. If cloning fails, the server stops with the error from git instead of starting an empty site.
- 🧠 **Package Manager Auto-Detect:** Supports `npm`, `pnpm`, and `yarn` with optional manual override.
- 🔒 **Secure:** Based on the official Pterodactyl Docker images (Parkervcp/Yolks).
- ✅ **Better Validation:** Restricts runtime mode to `start` or `dev` to prevent invalid command values.

## 🔧 Recommended Variables

- `NODE_RUN_ENV`: `start` for production, `dev` for development.
- `PACKAGE_MANAGER`: `auto` (default), `npm`, `pnpm`, or `yarn`.
- `NEXT_AUTO_UPDATE`: `patch` (default, for example 16.4.3 to 16.4.6), `minor` (stay within the current major version) or `off`.
- `NEXT_VERSION`: only used when the egg creates a brand new project. Existing projects keep the version in their own `package.json`.

## 📥 Installation Guide

1. **Download:** Get the `nextjs-egg.json` file from this repository (or copy the RAW link).
2. **Import:** Go to your Pterodactyl Admin Panel -> Nests -> Import Egg.
3. **Select Nest:** Choose the appropriate Nest (usually "NodeJS" or "Generic").
4. **Upload:** Upload `nextjs-egg.json` and complete the import wizard.
5. **Deploy:** You can now create new servers using this Egg!

## 🛠️ Troubleshooting

- **Install fails with package manager errors:** Set `PACKAGE_MANAGER` manually to `npm`, `pnpm`, or `yarn` instead of `auto`.
- **`pnpm` or `yarn` command not found:** Keep `PACKAGE_MANAGER=npm` or ensure Corepack is available in your selected Node image.
- **Unexpected dependency behavior:** Verify lockfiles in your project root (`package-lock.json`, `pnpm-lock.yaml`, or `yarn.lock`).
- **Server builds on every boot in production:** This is expected when `NODE_RUN_ENV=start`; use `dev` while iterating quickly.
- **Next.js shows a security vulnerability or upgrade prompt:** Keep `NEXT_AUTO_UPDATE` on `patch` (or `minor`) and restart the server. If the server pulls from git (`AUTO_UPDATE=1`), update Next.js in your repository instead; the egg will not change files that git manages.
- **Server not reachable from outside:** Confirm your panel allocation/port is correct; this Egg already binds Next.js to `0.0.0.0`.
- **Clone fails with `Write access to repository not granted` or `Authentication failed`:** Your token has no access to the repository. For a GitHub fine-grained token, select the repository and give it `Contents: Read-only`, then restart the server.

## ☕ Support My Work

If this Egg saved you time or fixed your server headaches, consider supporting my work! It helps me keep creating tools and fixes.

- **PayPal:** [paypal.me/JoopDev](https://paypal.me/JoopDev)
- **Website:** [JoopDev.com](https://www.joopdev.com)

**Author:** JoopDev (AKA. Vdbergjohannes)

---
*A fully optimized Pterodactyl Egg for Next.js. Features automatic dependency installation, auto-build on startup, and support for Node.js versions 18 through 26.*
