# Quantum-Safe TLS Lab — End-to-End Tutorial

This tutorial demonstrates how to establish HTTPS connections using quantum-safe cryptography with ML-KEM (formerly CRYSTALS-Kyber) using OpenSSL and the Open Quantum Safe provider ecosystem.

This lab protects TLS communications against future quantum computer attacks by using post-quantum key exchange.

---

## Overview

Traditional TLS key exchange mechanisms (e.g., elliptic-curve Diffie-Hellman) are vulnerable to future quantum attacks.

Quantum-safe TLS uses post-quantum cryptography such as ML-KEM to provide quantum-resistant key exchange.

This lab demonstrates quantum-safe TLS using:

• OpenSSL 3.x  
• Open Quantum Safe (liboqs)  
• oqs-provider  
• ML-KEM (FIPS 203; formerly CRYSTALS-Kyber)  

---

## Architecture

```text
Client
  │
  │ initiates TLS handshake
  ▼
Quantum-Safe TLS Server
  │
  │ performs ML-KEM key exchange
  ▼
Secure HTTPS Connection
```

---

## Prerequisites

Required software:

• OpenSSL 3.x  
• Open Quantum Safe (liboqs)  
• oqs-provider installed and accessible to OpenSSL  

Verify OpenSSL version:

```bash
openssl version
```

Verify oqs-provider is available:

```bash
openssl list -providers
```

Expected output includes:

```text
oqsprovider
default
```

Optional: list available ML-KEM algorithms from oqs-provider:

```bash
openssl list -kem-algorithms -provider oqsprovider
```

Expected output includes entries such as:

```text
mlkem512
mlkem768
mlkem1024
```

---

## Project Directory

```text
quantum-safe-tls-lab/
├── certs/
│   ├── server.cert.pem
│   └── server.key.pem
│
├── docs/
│   └── tutorial.md
│
├── README.md
└── LICENSE
```

Private keys must never be committed to source control.

---

## Step 1 — Navigate to Project Root

```bash
cd /Users/shinn/dev/quantum-safe-tls-lab
```

---

## Step 2 — Start Quantum-Safe TLS Server

Run the TLS server with oqs-provider enabled:

```bash
openssl s_server \
  -accept 8443 \
  -cert certs/server.cert.pem \
  -key certs/server.key.pem \
  -provider oqsprovider \
  -provider default \
  -www
```

The server now accepts TLS connections and can negotiate quantum-safe key exchange (ML-KEM).

Leave this terminal running.

---

## Step 3 — Connect Using Quantum-Safe TLS Client

Open a new terminal.

Navigate to project root:

```bash
cd /Users/shinn/dev/quantum-safe-tls-lab
```

Connect to the server with oqs-provider enabled:

```bash
openssl s_client \
  -connect localhost:8443 \
  -provider oqsprovider \
  -provider default
```

A successful handshake establishes an encrypted TLS connection.

---

## Step 4 — Verify Quantum-Safe Key Exchange

In the `openssl s_client` output, look for TLS 1.3 details such as:

```text
Protocol  : TLSv1.3
Cipher    : TLS_AES_256_GCM_SHA384
```

For quantum-safe verification, look for a key exchange indicator. Depending on OpenSSL/oqs-provider versions, this may be displayed as:

```text
Key Exchange: ML-KEM
```

Some builds may still display the legacy name:

```text
Key Exchange: Kyber
```

Kyber is the original research name. ML-KEM is the NIST standardized name (FIPS 203). Both refer to the same standardized family when referring to ML-KEM.

---

## Step 5 — Troubleshooting

### Provider not found

If you do not see `oqsprovider` in:

```bash
openssl list -providers
```

then OpenSSL is not loading oqs-provider. Confirm:

• oqs-provider is installed  
• OpenSSL can locate the provider module  
• environment variables (if used) are set correctly

### ML-KEM algorithms not listed

Check that oqs-provider exposes ML-KEM:

```bash
openssl list -kem-algorithms -provider oqsprovider
```

If ML-KEM entries do not appear, confirm your liboqs / oqs-provider versions support ML-KEM naming.

---

## Result

You have demonstrated:

• Quantum-safe TLS handshake  
• Post-quantum key exchange using ML-KEM (formerly CRYSTALS-Kyber)  
• Encrypted TLS 1.3 communication protected against future quantum threats  

This aligns with emerging enterprise and government cryptographic migration strategies.

---

## Next Steps

Possible enhancements:

• Hybrid classical + post-quantum TLS configurations  
• Integration with enterprise PKI for certificate issuance  
• Performance benchmarking and algorithm comparison  
• Containerized deployment for repeatable lab environments  

---

## License

MIT License