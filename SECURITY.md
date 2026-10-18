# Security Policy — IT-Community Sync Agent

IT-Community Sync Agent is distributed through this repository as signed binary releases.

## Verifying a download

- macOS builds are Developer-ID signed and notarized by Apple.
- Windows and component binaries ship with `.sha256` checksums in each
  release — verify before running.
- Auto-updates are fetched over verified TLS and signature-checked
  (EdDSA / SHA-256 with automatic rollback where supported).

## Reporting a vulnerability

Please report security issues privately to
**support@it-systems.es** — do not open a public issue for
vulnerabilities. We aim to acknowledge reports within 48 hours.

## Privacy

See https://it-community.online for the product privacy policy. These applications are
designed to run locally; where the product uses an account or cloud
service, only the data required for the feature is transmitted.
