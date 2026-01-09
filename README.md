# Self-Signed Certificate Generator

A browser-based tool for generating self-signed SSL/TLS certificates for development and internal use.

## Features

- Generate 2048-bit RSA certificates entirely in the browser
- Support for hostnames and IP addresses (IPv4/IPv6)
- Two output formats:
  - **PEM + KEY**: Zipped archive with `.crt` and `.key` files
  - **PKCS#12**: Single `.p12` bundle with password protection
- Configurable validity period (1-3650 days)
- No server-side processing - all cryptographic operations happen client-side

## Usage

1. Open `index.html` in a web browser
2. Enter the hostname or IP address for the certificate
3. Optionally set organization name and validity period
4. Choose output format (PEM or PKCS#12)
5. Click "Generate Certificate"
6. Download the generated certificate files

## Output Formats

### PEM + KEY (Default)

Downloads a ZIP file containing:
- `<hostname>.crt` - Certificate in PEM format
- `<hostname>.key` - Private key in PEM format
- `README.txt` - Usage instructions

### PKCS#12

Downloads a single `.p12` file containing both the certificate and private key, protected by a password (default: "changeit").

## Server Configuration Examples

### Apache
```apache
SSLCertificateFile /path/to/hostname.crt
SSLCertificateKeyFile /path/to/hostname.key
```

### Nginx
```nginx
ssl_certificate /path/to/hostname.crt;
ssl_certificate_key /path/to/hostname.key;
```

### Node.js
```javascript
const https = require('https');
const fs = require('fs');

const server = https.createServer({
  cert: fs.readFileSync('hostname.crt'),
  key: fs.readFileSync('hostname.key')
}, app);
```

## Dependencies

Uses CDN-hosted libraries:
- [node-forge](https://github.com/digitalbazaar/forge) - Cryptographic operations
- [JSZip](https://stuk.github.io/jszip/) - ZIP file generation

## Security Notice

These certificates are intended for **development and internal use only**. Browsers will display security warnings for self-signed certificates. For production environments, use certificates from a trusted Certificate Authority (CA).

## License

The Unlicense
