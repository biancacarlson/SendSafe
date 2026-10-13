# Send Safe

Send sensitive files without sending the key that unlocks them through the same channel.

Send Safe encrypts individual files or entire folders directly in your browser, packages them into a locked `.dat` file, and generates a unique key for each saved locked file. No account or server-side processing is required.

**Private by design.** Files are encrypted on your device. The page makes no network requests, and your files and keys are never uploaded, stored, or tracked by Send Safe.

One file: `index.html`. No build, no server, no dependencies.

## Features

- **File and folder encryption:** Lock individual files or entire folders in one package.
- **Unique access key:** Generate a unique 25-character key for each locked file.
- **Separate delivery:** Send the locked file and its corresponding key through different channels.
- **Configurable expiry:** Set a validity period of 1–30 days.
- **Browser-based:** No installation, account, or external dependencies.
- **Tamper detection:** Reject files that fail authenticated decryption.
- **Local processing:** Files are encrypted and decrypted on your device.

## How It Works

### Locking Files

1. Open the **Lock** tab and add files or an entire folder.
2. Choose how long the locked file remains valid, from 1 to 30 days.
3. Tap **Lock** to encrypt the contents.
4. Save or share the locked file, then copy its corresponding key.
5. Send the locked file and key through separate channels. For example, email the file and text the key.

### Unlocking Files

1. Open the **Unlock** tab and select the locked `.dat` file.
2. Enter the corresponding key and tap **Unlock**.
3. Save the recovered files to your device.
4. Delete the files when you no longer need them.

## Security

### Encryption

- **AES-256-GCM:** Files are encrypted locally using the browser's built-in Web Crypto API.
- **Unique encryption parameters:** Each lock generates a new random key and initialization vector (IV).
- **Random access key:** Each key contains 25 random characters, displayed in five groups of five, providing approximately 125 bits of entropy. Letter case, spaces, and dashes are ignored when entering the key.
- **Integrity verification:** AES-GCM authenticates the encrypted contents. An incorrect key or modified encrypted data causes decryption to fail.
- **No network requests:** A strict Content Security Policy blocks outbound connections, external scripts, and fonts. The page also disables referrer transmission and requests that search engines not index it.

### Expiry and Key Management

The selected expiry date is sealed inside the encrypted file. Send Safe checks that date before allowing the file to be unlocked.

Expiry is a convenience safeguard, not a cryptographic access restriction. The check relies on the device's clock and the Send Safe application. Someone with both the locked file and its key could use other software to decrypt the contents or bypass the expiry check.

Each saved locked file has its own unique key. Keep the key separate from the file and share it only with the intended recipient.

A lost key cannot be recovered. Create a new locked file from the original, unencrypted files if you lose the key.

## Limits and Safeguards

- **Maximum package size:** 50 MB per locked file.
- **Maximum file count:** 5,000 files per locked file.
- **Email size warning:** Files larger than 20 MB trigger a warning that the package may be too large for email.
- **Folder structure:** Folder structure is preserved. Unlocking a folder saves it as a `.zip` file. Multiple loose files can also be saved together as a `.zip`.

### Restricted File Types

Send Safe blocks file types that can execute code or conceal executable content, both when locking and when unlocking files.

Restricted types include:

- **Programs and installers:** `.exe`, `.msi`, `.dmg`, `.apk`, and similar formats.
- **Scripts:** `.js`, `.bat`, `.ps1`, `.sh`, and similar formats.
- **Web files:** `.html`, `.svg`.
- **Macro-enabled Office documents:** `.docm`, `.xlsm`, and similar formats.
- **Non-ZIP archives:** `.rar`, `.7z`, `.tar`, `.gz`, and similar formats.

ZIP archives are accepted only if their contents do not include restricted file types.

### File Naming

Locked files use the naming format:

```
Sent Safe YYYY-MM-DD ID.dat
```

The short ID appears alongside the corresponding key, making it easier to match each key to its locked file.

## Deployment

Send Safe consists of a single file: `index.html`.

There is no build process, server, package installation, or external dependency.

### Publish with GitHub Pages

1. Create a new public GitHub repository.
2. Upload `index.html` to the repository root.
3. Open **Settings → Pages**.
4. Under the build and deployment settings, select **Deploy from a branch**.
5. Choose the `main` branch and `/ (root)` folder, then save.
6. Open the published Pages URL, usually `https://<username>.github.io/<repo>/`.

Any static host that serves the page over HTTPS can be used. Web Crypto requires a secure context, such as HTTPS or localhost. GitHub Pages provides HTTPS.

### Browser Support

Use a current version of Chrome, Edge, Firefox, or Safari on desktop or mobile.

On desktop, files and folders can be dragged onto the page. On phones and tablets, use the **Files** and **Folder** buttons to select content.

## Trust and Updates

Both the sender and recipient use the hosted Send Safe page to lock and unlock files. Host it somewhere you control and trust. Anyone who can modify `index.html` can change what the application does.

Locked files created by earlier versions of Send Safe remain compatible with this version, provided the underlying file format and encryption handling remain compatible.
