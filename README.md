 🔐 Cryptbox 2.0 — Encrypted Virtual Filesystem with Secure Sharing

Client-Side Encryption · FUSE Virtual Filesystem · Zero-Knowledge Architecture · Secure File Sharing · Modern Web Dashboard**

Cryptbox 2.0 is a next-generation encrypted filesystem designed for secure, privacy-preserving cloud storage.
It transparently mounts a virtual filesystem using FUSE, encrypts all files client-side using AES-256-GCM, and stores only encrypted blobs in a backend directory compatible with Dropbox, iCloud, Google Drive, and all cloud sync systems.

This project is a modern continuation and enhancement of the original Cryptobox research developed by MIT students — evolving the architecture, strengthening security, and introducing a complete browser-based management dashboard.

---
## Features at a Glance

# 🔐 Transparent Encrypted Filesystem (FUSE)

* Mount a virtual directory for reading/writing plaintext.
* Backend storage stores only encrypted files.
* Fully supports macOS & Linux.
* Cloud-sync safe — zero plaintext leakage.

# 🛡 Strong Encryption

* AES-256-GCM authenticated encryption.
* PBKDF2-HMAC password-based key derivation.
* RSA-4096 public/private key pairs for secure sharing.
* Per-file signatures for tamper detection.

# 🔑 Modern Key Infrastructure

* Automatic RSA keypair creation.
* Private keys remain local only.
* Exportable public keys for sharing workflows.
* Deterministic, reproducible key derivation model.

# 🤝 Secure Sharing Protocol

Cryptbox 2.0 introduces a safe, cryptographically-sound sharing scheme:

* Wrap file keys using the recipient’s public key.
* Generate a “share bundle” containing encrypted metadata + signature.
* Receiver imports bundle to configure local decryption.
* No plaintext or passwords transmitted.

# ☁️ Cloud Sync Ready

Encrypted backend folder can be placed inside:

* Dropbox
* Google Drive
* iCloud Drive
* OneDrive
  No service ever receives plaintext.

# 🧱 Modular Architecture

Separated into clean modules:

* `encryption.py` — AES-GCM encryption
* `key_manager.py` — RSA keypair management
* `metadata.py` — manifest + integrity records
* `filesystem.py` — FUSE encrypted FS
* `sharing.py` — secure sharing logic
* `file_manager.py` — local file operations
* `config_manager.py` — persistent app configuration
* `gui/` — frontend dashboard
* `main.py` — CLI & Flask server entrypoint

---
# 🏗 System Architecture

```
              ┌─────────────────────────┐
              │     Web UI (Frontend)   │
              └────────────┬────────────┘
                           │ REST API
              ┌────────────▼────────────┐
              │      Flask Backend       │
              ├──────────┬───────────────┤
     Encrypt/Decrypt     │       Secure Sharing
              │          │
      ┌───────▼──────┐   │
      │ FileEncryptor │   │
      └───────┬──────┘   │
              │ AES-GCM   │ RSA-4096
      ┌───────▼──────────▼────────┐
      │       Metadata Manager     │
      └───────────┬───────────────┘
                  │
         ┌────────▼────────┐
         │    FUSE Mount    │
         └────────┬────────┘
                  │ plaintext
       ┌──────────▼────────────┐
       │   __enc__/ (ciphertext)│
       └────────────────────────┘
```
