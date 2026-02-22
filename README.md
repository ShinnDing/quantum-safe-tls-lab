# Quantum-Safe TLS Lab

## Overview

This project demonstrates quantum-safe Transport Layer Security (TLS) using post-quantum cryptography, specifically ML-KEM (Module-Lattice-Based Key-Encapsulation Mechanism), the NIST-standardized algorithm formerly known as CRYSTALS-Kyber.

This lab uses Open Quantum Safe (liboqs) and oqs-provider integrated with OpenSSL 3.x to establish TLS 1.3 connections protected by quantum-resistant key exchange.

Quantum-safe TLS protects communications from future quantum computer attacks and supports enterprise cryptographic migration strategies.

---

## Architecture

Quantum-safe TLS handshake:

```text
Client
  │
  │ Initiates TLS connection using ML-KEM key exchange
  ▼
Server
  │
  │ Performs post-quantum key encapsulation via oqs-provider
  ▼
Shared Secret Established
  │
  │ TLS 1.3 encrypted communication begins
  ▼
Secure Quantum-Resistant Connection
```

Trust model:

```text
Private PKI
├── Root CA
└── Server Certificate

ML-KEM
└── Provides quantum-safe key exchange
```

---

## Features

• Quantum-safe TLS handshake using ML-KEM (formerly CRYSTALS-Kyber)  
• Integration with Open Quantum Safe (liboqs)  
• OpenSSL 3.x configured with oqs-provider  
• TLS 1.3 secure communication  
• Hybrid and post-quantum cryptographic support  
• Demonstration of quantum-safe cryptographic migration  

---

## Technologies Used

OpenSSL 3.x  
Open Quantum Safe (liboqs)  
oqs-provider  
ML-KEM (FIPS 203, formerly CRYSTALS-Kyber)  
TLS 1.3  
X.509 Certificates  

---

## Security Benefits

Quantum-safe TLS provides:

• Resistance to quantum computer attacks  
• Protection against "harvest now, decrypt later" threats  
• Future-resistant key exchange mechanisms  
• Long-term confidentiality protection  

These protections are critical for enterprise, government, and identity infrastructure.

---

## Running the Quantum-Safe TLS Server

From project root:

```bash
cd /Users/shinn/dev/quantum-safe-tls-lab

openssl s_server \
  -cert certs/server.cert.pem \
  -key certs/server.key.pem \
  -www \
  -provider oqsprovider \
  -provider default
```

Server listens for quantum-safe TLS connections.

---

## Connecting with Quantum-Safe TLS Client

In a separate terminal:

```bash
cd /Users/shinn/dev/quantum-safe-tls-lab

openssl s_client \
  -connect localhost:443 \
  -provider oqsprovider \
  -provider default
```

---

## Verification

Successful connection output includes:

```text
Protocol  : TLSv1.3
Cipher    : TLS_AES_256_GCM_SHA384
Key Exchange: ML-KEM
```

Depending on OpenSSL version, the output may also display:

```text
Key Exchange: Kyber
```

Kyber refers to the original research name. ML-KEM is the official NIST-standardized name.

---

## Project Structure

```text
quantum-safe-tls-lab/
├── certs/
│   ├── server.cert.pem
│   └── server.key.pem
│
├── docs/
│   └── tutorial.md
│
├── scripts/
│
├── README.md
└── LICENSE
```

Private keys are excluded from version control.

---

## Learning Objectives

This project demonstrates:

• Post-quantum cryptography implementation  
• ML-KEM key exchange integration  
• Quantum-safe TLS configuration using OpenSSL  
• OpenSSL provider architecture  
• Cryptographic migration toward quantum-resistant algorithms  

These concepts are essential for modern identity and cryptographic infrastructure.

---

## Related Projects

private-pki-lab  
Private Certificate Authority infrastructure  

mtls-secure-api  
Mutual TLS authentication using private PKI  

oidc-identity-lab  
Identity federation using OpenID Connect  

---

## Standards Reference

NIST FIPS 203  
Module-Lattice-Based Key-Encapsulation Mechanism (ML-KEM)

https://csrc.nist.gov/publications/detail/fips/203/final

---

## Author

Stephanie Shinn  
IAM Consultant | PKI | Identity Security | Quantum-Safe Cryptography  

GitHub: https://github.com/ShinnDing

---

## License

MIT License