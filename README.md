# keepsake

A private page, hosted in public.

This repo contains exactly one thing: an AES-256-encrypted HTML file, served at **[maninae.github.io/keepsake](https://maninae.github.io/keepsake/)**. Without the passphrase, it's noise. With it, it's something personal to the owner — which is all this README will say about the contents.

---

## How it works

GitHub Pages can't password-protect a site, and Pages on a private repo still publishes publicly. So the protection lives in the file itself:

- **[StatiCrypt](https://github.com/robinmoisson/staticrypt)** encrypts the real page (AES-256, key derived from a passphrase) into a self-decrypting `index.html`
- Visiting the URL shows a password prompt; decryption happens entirely in the browser
- A share link with `#staticrypt_pwd=<hash>` unlocks it directly — the URL fragment never reaches any server
- "Remember me" stores the salted hash in localStorage so each device only asks once

```
private source repo ──(build: inline data, encrypt)──▶ this repo ──▶ GitHub Pages
        ▲                                                  │
   the real content                              ciphertext only — every
   never leaves here                             publish asserts no plaintext
```

> [!NOTE]
> The ciphertext is publicly fetchable, so security equals passphrase strength. This guards a personal page against the curious, not a vault against the determined.

## Notes to future self

- **Source & pipeline**: a private repo on this account; `pipeline/publish_pages.py` there builds and pushes here. Don't edit this repo by hand — it's overwritten on every publish.
- **Passphrase**: in the macOS keychain — search Keychain Access for *keepsake*.
- **Rotating access**: change the keychain passphrase and republish; every old link and remembered device is invalidated at once.

## License

The encryption shell is StatiCrypt (MIT). The encrypted payload is © the owner, all rights reserved.
