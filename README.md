# 🚀 Next.js Pterodactyl Egg (Network Binding Fix)

A custom, optimized Pterodactyl Egg for hosting **Next.js** applications.

This version resolves the common connectivity issue where Next.js servers show as "Ready" in the console but remain inaccessible via the browser/IP address due to incorrect network binding.

## 🧐 The Problem & Solution
By default, Next.js applications often bind to `localhost` (127.0.0.1). Inside a Docker container (which Pterodactyl uses), this prevents the application from being accessible from the outside world.

**This Egg fixes that** by automatically forcing the start command to listen on all interfaces (`0.0.0.0`), ensuring your site is immediately accessible after deployment.

---

## 🧩 Supported Versions

This Egg comes pre-configured with **all modern Node.js versions**, selectable during installation:

* **Node.js 24** (Latest)
* **Node.js 23**
* **Node.js 22** (LTS)
* **Node.js 21**
* **Node.js 20** (LTS)
* **Node.js 19**
* **Node.js 18** (LTS)

✅ **Next.js Compatibility:** Supports all modern Next.js versions (13, 14, 15, 16+) that run on these Node environments.

---

## ✨ Features

* **🔌 Instant Connectivity:** Pre-configured to listen on `0.0.0.0`, solving connection timeouts.
* **📦 Auto-Install:** Automatically runs `npm install` on startup if packages are missing.
* **⚙️ Auto-Build:** Runs `npm run build` to ensure your production build is fresh.
* **🔒 Secure:** Based on the official Pterodactyl Docker images (Parkervcp/Yolks).

## 📥 Installation Guide

1.  **Download:** Get the `egg-nextjs.json` file from this repository (or copy the RAW link).
2.  **Import:** Go to your **Pterodactyl Admin Panel** -> **Nests** -> **Import Egg**.
3.  **Select Nest:** Choose the appropriate Nest (usually "NodeJS" or "Generic").
4.  **Upload:** Upload the JSON file.
5.  **Deploy:** You can now create new servers using this Egg!

---

## ☕ Support My Work

If this Egg saved you time or fixed your server headaches, consider supporting my work! It helps me keep creating tools and fixes.

* **PayPal:** [paypal.me/vdbergjohannes](https://www.paypal.me/vdbergjohannes)
* **Website:** [vdbergjohannes.nl](https://vdbergjohannes.nl)

---

**Author:** vdbergjohannes
