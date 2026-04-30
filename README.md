# CipherHUB MCP Server

[![MCP](https://img.shields.io/badge/MCP-Server-blue)](https://tools.cipherhub.cloud/cipherhub/mcp)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)
[![Tools](https://img.shields.io/badge/Tools-31-orange)](#tools)

Production-grade cryptography toolkit exposing **31 cryptographic operations** via MCP (Model Context Protocol). 

## Overview

CipherHUB is a cryptography toolkit that enables AI agents to perform cryptographic operations without implementing algorithms themselves. It covers:

- **Classical Algorithms**: AES, RSA, ECC (SECP256R1/384R1/521R1, X25519, Ed25519)
- **Chinese National Standards**: SM2, SM3, SM4, ZUC
- **Post-Quantum Cryptography**: ML-KEM (FIPS 203), ML-DSA (FIPS 204), X25519+ML-KEM-768 Hybrid KEX
- **Interoperability**: Certified with AWS KMS (64/64) and Tencent Cloud KMS (39/39)

## Quick Start

### MCP Endpoint

```
https://tools.cipherhub.cloud/cipherhub/mcp
```

### Protocol

- **Type**: Streamable HTTP
- **Format**: JSON-RPC 2.0
- **Stateless**: No session required

### Example: Call a Tool

```bash
curl -X POST https://tools.cipherhub.cloud/cipherhub/mcp \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -d '{
    "jsonrpc": "2.0",
    "method": "tools/call",
    "params": {
      "name": "hash_sum",
      "arguments": {
        "plain_in_hex": "48656c6c6f",
        "required_hash_modes": ["SHA256"]
      }
    },
    "id": 1
  }'
```

### Example: List Resources

```bash
curl -X POST https://tools.cipherhub.cloud/cipherhub/mcp \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -d '{
    "jsonrpc": "2.0",
    "method": "resources/list",
    "id": 1
  }'
```

## Tools

### Hash Functions

| Tool | Description |
|------|-------------|
| `hash_sum` | SHA-1/224/256/384/512, SM3 |
| `hmac_sum` | HMAC with all hash algorithms |

### Symmetric Encryption

| Tool | Description |
|------|-------------|
| `block_cipher_encrypt` / `block_cipher_decrypt` | AES-128/256, SM4 (CBC mode) |
| `stream_cipher_encrypt` / `stream_cipher_decrypt` | AES-256-GCM, ChaCha20-Poly1305, SM4-GCM |
| `zuc_cipher` | ZUC-128 stream cipher |

### Asymmetric Cryptography

| Tool | Description |
|------|-------------|
| `rsa_generate_key` | Generate RSA key pair (2048/3072/4096 bits) |
| `rsa_encrypt` / `rsa_decrypt` | RSA encryption/decryption |
| `rsa_sign` / `rsa_verify` | RSA signatures |
| `ecc_generate_key` | Generate ECC key pair |
| `ecc_sign` / `ecc_verify` | ECDSA/EdDSA signatures |
| `ecc_key_exchange` | ECDH + HKDF key agreement |

### Chinese National Standards

| Tool | Description |
|------|-------------|
| `sm2_generate_key` | Generate SM2 key pair |
| `sm2_encrypt` / `sm2_decrypt` | SM2 encryption |
| `sm2_sign` / `sm2_verify` | SM2 signatures |

### Post-Quantum Cryptography

| Tool | Description |
|------|-------------|
| `ml_kem_keygen` | ML-KEM key generation |
| `ml_kem_encapsulate` / `ml_kem_decapsulate` | ML-KEM encapsulation/decapsulation |
| `ml_dsa_keygen` | ML-DSA key generation |
| `ml_dsa_sign` / `ml_dsa_verify` | ML-DSA signatures |
| `hybrid_kex_keygen` | X25519+ML-KEM-768 hybrid key exchange |

### Utility

| Tool | Description |
|------|-------------|
| `generate_random_data` | Generate secure random bytes |
| `data_padding` / `data_unpadding` | PKCS#7 padding |

## Resources

| URI | Description |
|-----|-------------|
| `cipherhub://algorithms` | Complete algorithm catalog |
| `cipherhub://tool-categories` | Tool categorization |
| `cipherhub://interop/aws-kms` | AWS KMS interoperability report |
| `cipherhub://interop/tencent-kms` | Tencent Cloud KMS interoperability report |
| `cipherhub://channel-implementation` | SDK channel protocol guide |

## Client Configuration

### Claude Desktop

Add to your Claude Desktop config:

```json
{
  "mcpServers": {
    "cipherhub": {
      "url": "https://tools.cipherhub.cloud/cipherhub/mcp"
    }
  }
}
```

### Cursor IDE

Add to your Cursor settings.

### Custom Client

Use any MCP-compatible client with the endpoint URL.

## API Documentation

- **OpenAPI**: https://tools.cipherhub.cloud/.well-known/openapi.yaml
- **llms.txt**: https://tools.cipherhub.cloud/llms.txt

## Web Interface

Interactive web UI available at: https://tools.cipherhub.cloud

## Author

**Yang X. CHEN**

- Blog: https://cipherhub.cloud
- GitHub: [@bowenerchen](https://github.com/bowenerchen)

## License

MIT License
