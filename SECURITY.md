# Security Policy

## Reporting a Vulnerability

If you discover a security vulnerability in GLYPH, please report it responsibly:

- **Email:** support@nuralyn.com
- **GitHub:** Use [Security Advisories](https://github.com/Nuralyn/GLYPH/security/advisories/new) to report privately

Please do not open public issues for security vulnerabilities. We will acknowledge receipt within 48 hours and provide a timeline for a fix.

---

## Scope

GLYPH is a **client-side-only** web application. There is no server, no backend, no database, and no telemetry. All computation happens in your browser.

The only network requests GLYPH makes are:

| Destination | Purpose | When |
|-------------|---------|------|
| `unpkg.com` | Load React, ReactDOM, Babel (with SRI hashes) | Page load |
| `fonts.googleapis.com` / `fonts.gstatic.com` | Load fonts | Page load |
| `api.anthropic.com`, `api.openai.com`, `generativelanguage.googleapis.com`, `api.deepseek.com` | AI interpretation | Only when you click "Interpret" with your own API key |
| `portal.opentopography.org` | Elevation data import | Only when you request terrain data with your own API key |

All external requests are governed by a strict Content Security Policy (CSP) that prevents connections to any unlisted domain.

---

## Security Measures

### Content Security Policy (CSP)
GLYPH ships with a restrictive CSP header that limits script sources, connection targets, and frame embedding. The CSP allowlists only the specific domains listed above.

### Subresource Integrity (SRI)
All externally loaded scripts (React, ReactDOM, Babel) include SRI hashes that verify the file has not been tampered with. If a CDN serves modified code, the browser will refuse to execute it.

### Permissions Policy
GLYPH explicitly disables browser APIs it does not use: camera, microphone, geolocation, and payment.

### Referrer Policy
Set to `no-referrer` to prevent URL leakage to external services.

### Input Validation
All user input (binary grids, CSV coordinates, AAI Grid files) is validated with dimension limits (500x500, 62,500 cells max), format checks, and row consistency verification. Error messages redact long token-like strings and API key patterns.

### No Cookies
GLYPH does not set or read any cookies.

---

## Known Limitations

### Babel Standalone requires `unsafe-eval`
The CSP includes `'unsafe-eval'` because Babel Standalone transpiles JSX to JavaScript at runtime in the browser, which requires `eval()`. This is a deliberate trade-off to maintain the zero-build-step, single-file architecture. No application code uses `eval()` directly.

### `unsafe-inline` for styles
Because GLYPH is a single HTML file, all CSS is inline. This requires `'unsafe-inline'` in the CSP `style-src` directive.

### API key storage
- **Default:** API keys are stored in React state (memory only). They are lost when you close or refresh the page. This is the recommended mode.
- **Optional persistence:** If you check "Remember my API keys," keys are stored in `localStorage` in **plaintext**. This is a convenience feature, not a security feature. Anyone with access to your browser's developer tools or filesystem can read them. Do not use this on shared or public computers.

### Gemini API key in URL
The Google Gemini API requires the API key as a URL query parameter. This means the key may appear in browser history. This is a limitation of the Gemini API design, not GLYPH.

---

## Supported Versions

GLYPH is distributed as a single HTML file. We recommend always using the latest version from the [releases page](https://github.com/Nuralyn/GLYPH/releases) or [glyph.nuralyn.com](https://glyph.nuralyn.com).

| Version | Supported |
|---------|-----------|
| Latest release | Yes |
| Older releases | Best-effort |
