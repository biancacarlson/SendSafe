# Send Safe

Lock files or a whole folder with a one-time key, send the locked file, and let the other person unlock it. Everything happens in the browser. Nothing is uploaded, stored, or tracked.

One file: `index.html`. No build, no server, no dependencies.

## How it works

**Locking**

1. Open the **Lock** tab and add files or an entire folder.
2. Choose how long the file stays valid, from 1 to 30 days.
3. Tap **Lock**, then **Save** (or **Share**) the locked file and **Copy** the key.
4. Send the locked file and the key through different channels, for example the file by email and the key by text.

**Unlocking**

1. Open the **Unlock** tab and choose the locked file.
2. Paste the key and tap **Unlock**.
3. **Save** the files. Delete them when you're done.

## Security

- Files are bundled and encrypted on the device with AES-256-GCM through the browser's built-in Web Crypto. Each lock uses a new random key and a new random IV.
- The key is 25 random characters (about 125 bits), shown as five groups of five. Case, dashes and spaces are ignored when it's pasted back in.
- GCM authenticates the file, so a damaged or tampered file fails to unlock instead of producing bad output.
- The page can't talk to the network. A strict Content Security Policy blocks all outside requests, scripts, and fonts, and the page sends no referrer and asks search engines not to index it.
- A lost key can't be recovered. Make a new locked file instead.

**Expiry.** The expiry date is sealed inside the encrypted file, and Send Safe refuses to open an expired file. This is a courtesy check, not a cryptographic one. It uses the device's clock, and anyone who has both the file and the key and uses other software could still decrypt it. Treat the key as the real access control, and delete files you no longer need.

## Limits and safeguards

- Up to 50 MB and 5,000 files per locked file. Above 20 MB you'll see a "big for email" warning.
- Folder structure is kept. Unlocking a folder saves it as a `.zip`; several loose files can be saved together the same way.
- Files that can run code or hide it are refused when locking and blocked when unlocking: programs and installers (`.exe`, `.msi`, `.dmg`, `.apk`…), scripts (`.js`, `.bat`, `.ps1`, `.sh`…), web files (`.html`, `.svg`), macro-enabled Office files (`.docm`, `.xlsm`…), and archives other than `.zip` (`.rar`, `.7z`, `.tar`, `.gz`). A `.zip` is accepted only if nothing inside it is on that list.
- Locked files are named `Sent Safe YYYY-MM-DD ID.dat`. The short ID appears next to the key so the two are easy to match.

## Deploy

1. Create a new public repository.
2. Upload `index.html` (this README is optional).
3. Go to **Settings → Pages → Deploy from branch** and choose `main` / `/ (root)`.
4. Share the Pages link, usually `https://<username>.github.io/<repo>/`.

Any static host works the same way. The page needs HTTPS or localhost for Web Crypto to be available, and GitHub Pages provides HTTPS. Use a current version of Chrome, Edge, Firefox, or Safari on desktop or mobile. Dropping folders onto the page works on desktop; on phones, use the **Files** and **Folder** buttons.

## Trust and updates

The sender and the receiver both use the same hosted page, so host it somewhere you control and trust. Anyone who can change `index.html` can change what the page does. Locked files made by earlier versions of the page still open in this one.
