# E VPN  

A complete, end-to-end VPN software solution built from the ground up using **C++** and **Python**.  
This project provides a secure, encrypted tunnel for all internet traffic, featuring a robust backend, a background Windows service, and a user-friendly graphical interface.  
It’s designed as a comprehensive, educational example of how professional VPNs are engineered.  

---

## ✨ Features  

- **Secure Encrypted Tunnel** – TLS 1.2+ handshake & AES-256 encryption for all traffic.  
- **Low-Level Packet Capture** – TAP virtual network adapter routes all IP packets through the VPN.  
- **Background Windows Service** – Persistent, silent client service independent of UI.  
- **Graphical User Interface (GUI)** – Python + Tkinter UI for credentials, server selection & control.  
- **Dynamic Server List** – Flask API provides up-to-date server locations.  
- **Professional Kill Switch** – WFP-based kill switch blocks all non-VPN traffic on disconnect.  
- **Cross-Platform Server** – Core server runs on Linux using C++.  

---

## 🛠 Technology Stack  

- **Client Core:** C++  
- **Server Core:** C++  
- **User Interface:** Python 3, Tkinter  
- **Server List API:** Python 3, Flask  
- **Cryptography:** OpenSSL (TLS + AES-256)  
- **Windows Networking:** TAP-Windows Driver, Windows Filtering Platform (WFP)  
- **Server Networking:** Raw Sockets (Linux)  

---

## ⚡ How to Build and Run  

### Prerequisites  
- **Server (Linux):** `g++`, `libssl-dev`  
- **Client (Windows):** Visual Studio (C++ tools), OpenSSL for Windows, TAP-Windows Driver  
- **UI (Windows):** Python 3, `requests`, `pyinstaller`  
- **API Server:** Python 3, `flask`  

---

### 1. VPN Server (Linux)  
```bash
# Generate certs
openssl req -x509 -nodes -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365  

# Compile
g++ vpn_server.cpp -o vpn_server -lpthread -lssl -lcrypto  

# Run as root
sudo ./vpn_server  

# Compile vpn_service.cpp (MSVC command in source) → vpn_service.exe  

# Create directory
mkdir C:\MyVPN\
move vpn_service.exe C:\MyVPN\

# Install service
sc create MyVPNService binPath= "C:\MyVPN\vpn_service.exe"

# Update VPN_SERVERS in server_api.py  
python server_api.py  

# Update API_URL & CONFIG_PATH in vpn_ui.py  
python vpn_ui.py  

🔒 Security Notes

Currently uses hardcoded credentials (user:pass). Replace with a secure DB in production.

TLS ensures unique session keys with forward secrecy.

Kill switch rules persist until service restarts, ensuring protection even on crash.

🚀 Future Improvements

Database Integration: Secure user authentication with SQLite/MySQL.

Kill Switch Integration: Merge vpn_killswitch.cpp into vpn_service.cpp.

UI Enhancements: Real-time bandwidth monitoring & detailed status.

Installer: Windows installer for TAP driver, service, and UI.
