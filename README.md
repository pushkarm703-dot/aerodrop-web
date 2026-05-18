# ⚡ AeroDrop
> **Zero Cloud. Zero Wait. Pure Mesh.**

AeroDrop is a high-performance, cross-platform P2P ecosystem designed to bridge the gap between Windows and Android. It bypasses the cloud entirely, using local mesh networking to sync files and clipboards at the absolute speed of your router.

![Flutter](https://img.shields.io/badge/Flutter-%2302569B.svg?style=for-the-badge&logo=Flutter&logoColor=white)
![Firebase](https://img.shields.io/badge/Firebase-039BE5?style=for-the-badge&logo=Firebase&logoColor=white)
![Dart](https://img.shields.io/badge/dart-%230175C2.svg?style=for-the-badge&logo=dart&logoColor=white)

---

## 🚀 The Vision
Most sync tools rely on middle-man servers (The Cloud). **AeroDrop** kills the middleman. By establishing direct **TCP Sockets** over local infrastructure, data moves with zero latency and maximum privacy. If your devices are on the same Wi-Fi or Hotspot, they are one single workspace.

## ✨ Key Features
* **📡 Zero-Internet Transfer:** Move gigabytes of data without touching a single byte of your data plan.
* **📋 Single Brain (Universal Clipboard):** Copy a link or snippet on Windows; it’s already on your Android clipboard.
* **🔐 Secure Protocol:** Rolling 4-digit PINs, SHA-256 hashing, and HMAC challenge-response handshakes.
* **🌐 Smart Discovery:** Uses mDNS (Multicast DNS) to find peers instantly without needing to type IP addresses.
* **💻 Native Windows Auth:** Implements a custom Loopback Server for Google OAuth2, bypassing the limitations of desktop webviews.

---

## 🛠 Technical Architecture
AeroDrop is built on a custom mesh architecture designed for reliability and speed.

### 1. Peer Discovery (mDNS)
Utilizes the `nsd` (Network Service Discovery) protocol. The desktop app acts as a service provider, broadcasting its presence on `_aerodrop._tcp`. The mobile client scans the local network and resolves the socket address automatically.

### 2. The Socket Engine
Communication is handled via raw **Transmission Control Protocol (TCP)**. 
* **Data Streaming:** Files are broken into chunks and streamed through `ServerSocket` and `Socket` objects to prevent memory overflow on large transfers.
* **Async Handling:** Utilizes Dart's `Stream` API to provide real-time progress updates and UI reactivity.

### 3. Windows Loopback Auth
Since Google blocks embedded webviews in desktop apps, AeroDrop spins up a temporary **Internal Web Server** on `localhost:8080` to intercept the OAuth2 authorization code from the system browser, ensuring a secure and native login experience.

---

## 🛡 Security Protocol
Security isn't an afterthought; it's the foundation.
1.  **Handshake:** Devices exchange a unique challenge string.
2.  **Verification:** The receiver must provide a proof of PIN ownership using an **HMAC (Hash-based Message Authentication Code)**.
3.  **Isolation:** No data is stored on any server. The only point of failure is your own local network.

---

## 📦 Installation & Setup

### Windows
1. Download the `Aerodrop_Setup.exe` from the [Releases](https://aerodrop-web.vercel.app/) page.
2. Run the installer and follow the modern setup wizard.
3. Sign in with Google to initialize your mesh identity.

### Android
1. Download the `app-release.apk`.
2. Enable "Install from Unknown Sources" in your Android settings.
3. Install and sync.

---

## 🛠 Development
If you want to contribute or build from source:

```bash
# Clone the repo
git clone [https://github.com/yourusername/p2pcommunication.git](https://github.com/yourusername/p2pcommunication.git)

# Install dependencies
flutter pub get

# Run the app
flutter run
