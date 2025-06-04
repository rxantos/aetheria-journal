# Secure Communication System - Design Document

## Objective

Design a secure and private communication system starting from basic encrypted messaging (initially over IRC), with a future path toward full peer-to-peer (P2P) architecture. The solution should be cross-platform, efficient, and modular.

## Phase 0: Foundations and Planning

### Goals

* Identify all necessary components.
* Determine required libraries.
* Define a modular and extensible architecture.
* Ensure cross-platform considerations (Windows, Linux, etc).

## Phase 1: Encryption Core

### Objective

Build a standalone AES-256 encryption module with CPU acceleration support.

### Requirements

* AES-256 in CBC or GCM mode.
* Support for CPU acceleration (AES-NI).
* Secure random key and IV generation.
* Minimal and efficient API.

### Candidate Libraries

* [OpenSSL](https://www.openssl.org/): Industry standard; supports AES-NI, TLS, and more.
* [libsodium](https://libsodium.gitbook.io/doc/): High-level and easy to use; built on NaCl.

### Tasks

* [ ] Benchmark OpenSSL and libsodium for AES-256 on target systems.
* [ ] Create a minimal interface to encrypt/decrypt messages.
* [ ] Securely manage and store session keys.

## Phase 2: Transport via IRC (Prototype)

### Objective

Use a tag-based system over an existing IRC server (e.g., UnrealIRCd) to exchange encrypted messages.

### Features

* Encrypted message wrapper: `ENC:<base64-ciphertext>`.
* Identify user sessions securely.
* Ignore plaintext fallback for max privacy.

### Tasks

* [ ] Integrate encryption core.
* [ ] Create a plugin or client wrapper for existing IRC client.
* [ ] Tag/untag messages with ENC tags.

### Limitations

* Requires trusted server.
* Not resistant to MITM.

## Phase 3: Peer-to-Peer Architecture

### Objective

Remove reliance on centralized IRC server; move to decentralized peer-to-peer.

### Features

* Peer discovery.
* Encrypted message transport.
* NAT traversal.
* Optional I2P or Tor support.

### Candidate Libraries / Tools

* [libp2p](https://libp2p.io/): P2P networking.
* [i2pd](https://github.com/PurpleI2P/i2pd): C++ implementation of I2P.
* [miniupnp](https://miniupnp.tuxfamily.org/): NAT traversal via UPnP.

### Tasks

* [ ] Evaluate libp2p vs custom P2P layer.
* [ ] Build peer handshake and identity exchange.
* [ ] Secure routing and fallback to onion-routing.

## Phase 4: Optional Extensions

### Audio Communication (Experimental)

* Encrypted VoIP (possibly with [Opus](https://opus-codec.org/)).
* Latency concerns must be addressed.

### Forward Secrecy

* Use ephemeral keys (e.g., X25519).

### Encrypted Storage

* Secure local chat history with key management.

### Replay and Audit

* Optional audit logs with forward secrecy guarantees.

## Cross-Platform Considerations

* Abstract OS-specific code.
* Prefer libraries with wide support.
* Build system: CMake or Meson.

## Final Notes

This system is designed to evolve from an encryption testbed over IRC to a full privacy-respecting decentralized communication tool. By taking a layered and testable approach, we ensure clarity, security, and maintainability.

---

Next Step: List all required libraries for Windows 64-bit first, then expand to general compatibility.
