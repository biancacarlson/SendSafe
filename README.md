# Send Safe

Send Safe lets you encrypt and send sensitive files in seconds. Uploaded docs are encrypted entirely in your browser into a secure `.dat` file, with a unique 25-character key generated for each one. Because it is a single-file application with zero external dependencies, your data never touches a server.

## Quick Start

### 1. Lock a File 🔒

1. Go to the **Lock** tab and upload your files or folders.
2. Set an expiration date (1–30 days).
3. Click **Lock**, download the generated `.dat` file, and copy the key.

> **Golden Rule:** Share the `.dat` file separately from the key. For example, email the file and text the key.

### 2. Unlock a File 🔓

1. Go to the **Unlock** tab and upload the `.dat` file.
2. Paste the 25-character key and click **Unlock**.
3. Download your decrypted files.

## Features

- 💻 **100% Client-Side:** No accounts, no tracking, and zero network requests.
- 📁 **Folder Support:** Preserves full folder directories (downloads as a `.zip`).
- 🔑 **High-Entropy Keys:** Generates a unique 25-character key split into 5 blocks.
- 🛡️ **Tamper Proof:** Built-in authenticated decryption catches modified files instantly.
- 🚫 **Code Execution Protection:** Proactively blocks potentially unsafe file extensions.

## System Limits & Guardrails

| Guardrail | Limit / Behavior |
| --- | --- |
| Max package size | 50 MB per `.dat` file |
| Max file count | 5,000 files per package |
| Email warning | Triggers a warning if a package exceeds 20 MB |
| Output naming | `Sent Safe YYYY-MM-DD ID.dat` |

### Restricted File Types

To protect users from malicious payloads, Send Safe blocks the encryption and decryption of:

| Category | Extensions |
| --- | --- |
| Executables / installers | `.exe`, `.msi`, `.dmg`, `.apk` |
| Scripts | `.js`, `.bat`, `.ps1`, `.sh` |
| Web languages | `.html`, `.svg` |
| Macros | `.docm`, `.xlsm` |
| Non-ZIP archives | `.rar`, `.7z`, `.tar`, `.gz` |

ZIP files are allowed as long as they don't contain restricted types.

## Security Architecture

### Cryptographic Implementation

- **Algorithm:** AES-256-GCM, managed natively through the browser's Web Crypto API.
- **Parameters:** Every operation generates a brand-new, cryptographically random initialization vector (IV) and key.
- **Lenient input:** The unlock field ignores spaces, dashes, and letter case, which makes it easy to enter on mobile.

### Expiry Handling

The expiry timestamp is sealed cryptographically inside the encrypted file, and Send Safe checks it before unlocking.

> ⚠️ **Note:** Lost keys cannot be recovered. If you lose one, lock the original files again to get a new key.

### Network Isolation

A strict, embedded Content Security Policy (CSP) locks down the environment:

- Disables all external scripts, fonts, and stylesheets.
- Prevents data exfiltration by blocking all outbound connection types.
- Disables HTTP referrers and asks search engine crawlers not to index the page.

## Easy Deployment

Send Safe is built entirely inside a single `index.html` file, so deployment needs no build pipeline, node modules, or servers.

### Option A: GitHub Pages

1. Create a public GitHub repository.
2. Drop `index.html` straight into the repository root.
3. Head over to **Settings ➡️ Pages**.
4. Set the source to **Deploy from a branch**, choose `main` / `(root)`, and hit **Save**.

### Option B: Local / Self-Hosted

Serve it from any static server. Web Crypto requires a secure context (`https://` or `localhost`) to function.

```bash
# Example: quickly serve locally with Python
python3 -m http.server 8080
```

## Compatibility

- **Browsers:** Modern versions of Chrome, Edge, Firefox, and Safari (desktop and mobile).
- **UI controls:** Drag-and-drop on desktop, and the native file picker on mobile.

## ⚖️ Legal Disclaimer & Liability Disclosure

### 1. "As-Is" Software Provision

Send Safe is provided on an **"AS IS" and "AS AVAILABLE" basis**, without warranties of any kind, either express or implied, including but not limited to warranties of merchantability, fitness for a particular purpose, or non-infringement.

### 2. Limitation of Liability

In no event shall the authors, developers, copyright holders, or hosts of this webpage or repository be liable for any claims, damages, or other liabilities, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software. This includes, without limitation, damages for:

- **Data loss:** Permanent loss or corruption of files during encryption or decryption.
- **Key loss:** Inability to access encrypted files due to a forgotten, altered, or lost 25-character access key (keys are mathematically unrecoverable).
- **Security bypasses:** Bypassing of the local device-clock-dependent expiry system by sophisticated actors.

### 3. User Responsibility & Content Compliance

Send Safe is a neutral, 100% client-side privacy tool. It does not look at, store, log, or transmit user data. Because all processing occurs strictly on your local device, the operators of this software have zero visibility into, control over, or access to your files.

By using this tool, you acknowledge and agree that:

- You are solely responsible for the content of the files you encrypt and distribute.
- You will not use this tool to transmit, package, or hide illegal material, malware, or content that violates intellectual property or regional laws.
- You assume all legal and regulatory risks associated with the distribution and receipt of your data.

### 4. Cryptographic Export Control Notice

This software uses strong symmetric encryption (AES-256-GCM) managed through the native web browser environment. Depending on your country or jurisdiction, importing, exporting, hosting, or using software capable of 256-bit encryption may be subject to restricted legal regulations. It is your responsibility to ensure compliance with local import/export control laws before hosting or operating this application.
