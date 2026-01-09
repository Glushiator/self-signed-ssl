# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/claude-code) when working with code in this repository.

## Project Overview

This is a single-page web application that generates self-signed SSL/TLS certificates entirely in the browser. There is no backend - all cryptographic operations are performed client-side using the node-forge library.

## Architecture

- **Single file application**: All HTML, CSS, and JavaScript are contained in `index.html`
- **No build process**: The application runs directly in the browser without compilation
- **CDN dependencies**: Uses externally hosted libraries (forge, JSZip)

## Key Components

### Libraries (loaded via CDN)
- `forge` (node-forge): RSA key generation, certificate creation, PKCS#12 encoding
- `JSZip`: Creating ZIP archives for PEM format output

### Main Functions
- `generateCertificate()`: Core function that generates the RSA keypair and X.509 certificate
- `downloadCertificate()`: Triggers browser download of the generated files
- `setStatus()` / `hideStatus()`: UI feedback utilities

### Certificate Generation Flow
1. Generate 2048-bit RSA key pair using `forge.pki.rsa.generateKeyPair()`
2. Create X.509 certificate with subject/issuer attributes
3. Set extensions (basicConstraints, keyUsage, extKeyUsage, subjectAltName)
4. Sign with SHA-256
5. Export as PEM (zipped) or PKCS#12 format

## Development Notes

- The app uses `setTimeout` to allow UI updates during key generation (CPU-intensive)
- IP addresses are detected via regex and added to subjectAltName as type 7 (IP), hostnames as type 2 (DNS)
- Default P12 password is "changeit" if not specified
