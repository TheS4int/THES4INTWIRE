# Privacy information (v1.24)

THES4INTWIRE's principal monitoring runs on the user's device. Local IOC matching does not transmit the observed address list to cloud reputation services.

Optional features and disclosures:
- PTR lookups contact configured DNS resolvers; RDAP lookups contact public registration data services.
- VirusTotal and AbuseIPDB requests are opt-in per analysis and disclose the selected public IP address and the corresponding provider API key to that service. See the services' policies before querying.
- Browser Bridge sends tab metadata and observed traffic measurements to a pairing-protected local listener at 127.0.0.1:38471. The bridge's permissions vary by browser, and Chromium's debugger interface can display a browser warning.
- API keys are handled in the active app session and are not intentionally written to disk by this feature. Review applicable runtime and OS diagnostics settings.

This notice describes application behavior, not third-party provider data retention or an audited privacy guarantee.
