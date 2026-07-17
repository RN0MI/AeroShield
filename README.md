# AeroShield

**A Lightweight Cryptographic Layer for Securing Processed Data and Metadata in UAV Detection Systems**

AeroShield is a cybersecurity solution designed to protect processed UAV detection data and metadata using lightweight cryptographic techniques. The system ensures confidentiality, integrity, authenticity, replay protection, and secure forensic logging while maintaining real-time performance.

---

## Features

- Secure key exchange using X25519
- Digital signatures using Ed25519
- ChaCha20-Poly1305 authenticated encryption
- SHA-256 integrity verification
- Replay attack protection
- Secure metadata validation
- AI-based UAV classification
- Blockchain-based forensic logging

---

## Technologies

- Python
- Docker
- X25519
- Ed25519
- HKDF-SHA256
- ChaCha20-Poly1305
- SHA-256

---

# Installation

### Clone the Drone Audio Dataset

```bash
git clone https://github.com/saraalemadi/DroneAudioDataset.git
```

### Create a Python Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Build the Docker Image

```bash
cd ~/Aeroshield/aeroshield_cloud
sudo docker build -t aeroshield-cloud .
```

---

# Running AeroShield

### UAV Audio Sample

```bash
bash ~/Aeroshield/aeroshield_cloud/run.sh \
~/Aeroshield/DroneAudioDataset/Binary_Drone_Audio/yes_drone/B_S2_D1_068-bebop_003_.wav
```

### Non-UAV Audio Sample

```bash
bash ~/Aeroshield/aeroshield_cloud/run.sh \
~/Aeroshield/DroneAudioDataset/Binary_Drone_Audio/unknown/1-977-A-392.wav
```

---

# Key Storage

Receiver private keys are stored inside an encrypted **eCryptfs** vault.

```text
~/Aeroshield_keys/keys_vault
```

Mount the vault before execution:

```bash
sudo mount -t ecryptfs \
~/Aeroshield_keys/keys_vault \
~/Aeroshield_keys/keys_vault
```

Receiver key files are protected using restricted file permissions (`chmod 600`).

When the vault is locked, private keys remain encrypted on disk. After mounting with the correct passphrase, the Cloud Layer can securely access the receiver keys for package verification and decryption.

---

# Cloud Processing Workflow

```text
secure_package.json
        │
        ▼
[1] Replay Protection
[2] Nonce Validation
[3] Key Loading
[4] Session Key Derivation (X25519 + HKDF-SHA256)
[5] Metadata Verification (Ed25519)
[6] Spectrogram Decryption (ChaCha20-Poly1305)
[7] SHA-256 Integrity Validation
[8] AI/ML Classification
[9] Blockchain Logging
[10] Ground Station Alert
```

---

# Output Files

### Package Output

```text
*_secure_package.json
*_receiver_keys.json
package_counter.json
```

### Logs

```text
audit_log.jsonl
data_log.jsonl
blockchain.jsonl
```

### Key Vault

```text
keys_vault/
├── A0001.key
├── A0002.key
└── *_receiver_keys.json
```

---

# Cryptography

| Component | Algorithm |
|-----------|-----------|
| Key Exchange | X25519 (RFC 7748) |
| Session Key Derivation | HKDF-SHA256 |
| Digital Signature | Ed25519 (RFC 8032) |
| Authenticated Encryption | ChaCha20-Poly1305 (RFC 7539) |
| Integrity Verification | SHA-256 |

---

# Logs

```text
aeroshield_output/logs/
```

| File | Description |
|------|-------------|
| audit_log.jsonl | Cryptographic verification and security events |
| data_log.jsonl | AI classification results and alerts |
| blockchain.jsonl | Tamper-evident forensic records |

---

# Authors

- Raneem Alharbi
- Renad Awari
- Ahad Alanizi
- Rawan Abdulsalam
- Wesam Aljohani
