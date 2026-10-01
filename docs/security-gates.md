# Security Gates

- Terraform fmt
- IaC scan
- Container scan
- Secret scan
- Runtime pentest (DAST)
- SARIF upload

## Runtime pentest (DAST)

The scans above are static: they read code, IaC and images at rest. The runtime
gate (`templates/github-actions-runtime-pentest.yml`) adds dynamic coverage by
running an autonomous penetration test against a deployed instance and proving
each finding with a real exploit, then uploading results as SARIF.

Engine: Darkmoon, an open source (GPL-3.0) autonomous pentest platform. Run it
after a deploy against a staging/preview URL you are authorized to test. The gate
is a no-op until `DARKMOON_BASE_URL` / `DARKMOON_API_TOKEN` are configured, so it
can be adopted incrementally.
