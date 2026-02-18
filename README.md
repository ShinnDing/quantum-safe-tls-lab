# Quantum-Safe TLS Lab

## Overview

This project demonstrates quantum-safe Transport Layer Security (TLS) using post-quantum cryptography, specifically CRYSTALS-Kyber, implemented via Open Quantum Safe (liboqs) and oqs-provider with OpenSSL.

This lab shows how traditional TLS key exchange mechanisms can be replaced or augmented with quantum-resistant algorithms to protect against future quantum computer attacks.

---

## Architecture

Quantum-safe TLS handshake:

```text
Client
  │
  │  Initiates TLS connection using Kyber key exchange
  ▼
Server
  │
  │  Responds with quantum-safe key exchange parameters
  ▼
Shared Secret Established
  │
  │  Encrypted TLS communication begins
  ▼
Secure Quantum-Resistant Connection
```

---

## Features

• Quantum-safe TLS handshake using CRYSTALS-Kyber  
• Integration with Open Quantum Safe (liboqs)  
• OpenSSL configured with oqs-provider  
• Hybrid and post-quantum key exchange support  
• Secure client-server communication  

---

## Technologies Used

OpenSSL  
Open Quantum Safe (liboqs)  
oqs-provider  
CRYSTALS-Kyber  
TLS 1.3  

---

## Security Benefits

• Resistant to attacks from quantum computers  
• Protection against "harvest now, decrypt later" attacks  
• Future-proof cryptographic key exchange  
• Strong cryptographic confidentiality  

---

## Example Commands

Start quantum-safe TLS server:

```bash
openssl s_server \
  -cert server-cert.pem \
  -key server-key.pem \
  -www \
  -provider oqsprovider \
  -provider default
```

Connect using quantum-safe TLS client:

```bash
openssl s_client \
  -connect localhost:443 \
  -provider oqsprovider \
  -provider default
```

---

## Verification

Example output showing quantum-safe key exchange:

```text
Key Exchange: Kyber
Protocol: TLSv1.3
Cipher: TLS_AES_256_GCM_SHA384
```

---

## Learning Objectives

This project demonstrates understanding of:

• Post-quantum cryptography concepts  
• CRYSTALS-Kyber key exchange  
• Quantum-safe TLS implementation  
• OpenSSL provider architecture  
• Future cryptographic migration strategies  

---

## Repository Structure

```text
quantum-safe-tls-lab/
├── server/
├── client/
├── certs/
├── scripts/
├── LICENSE
└── README.md
```

---

## Future Improvements

• Hybrid classical and post-quantum TLS configuration  
• Performance comparison testing  
• Automated deployment scripts  
• Integration with enterprise PKI  

---

## Author

Stephanie Shinn  
IAM Consultant | PKI | Identity Security | Quantum-Safe Cryptography  

---

## License

MIT License
