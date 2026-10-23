# Two download website

A responsive, dark minimalist static download page for Two. Host it for free with GitHub Pages.

## 1. Create a website repository

Create a separate **public** GitHub repository, for example `two-downloads`. Keep the app/source repository private if it contains private configuration or code. Copy `index.html` into the root of the new repository.

## 2. Connect the Windows download

Open `index.html` and find the `DOWNLOADS` object near the bottom:

```js
const DOWNLOADS = {
  windows: "WINDOWS_DOWNLOAD_URL",
  mac: "MAC_DOWNLOAD_URL",
  iphone: "IPHONE_DOWNLOAD_URL",
  version: "v0.1.0",
  project: "https://github.com/isaache9999-dotcom/two-chat-app"
};
```

Replace `WINDOWS_DOWNLOAD_URL` with a stable HTTPS URL to the actual `.msi` or `.exe` installer.

Recommended: create a GitHub Release in a **public download repository**, upload the installer as a Release asset, and use its asset URL. A GitHub Actions artifact URL is temporary and may require sign-in. If your app repository is private, friends generally cannot access its private release assets; do not make your whole source repository public just to share the installer.

## 3. Enable GitHub Pages

In the public website repository:
1. Open **Settings → Pages**.
2. Under **Build and deployment**, choose **Deploy from a branch**.
3. Select branch `main` and folder `/(root)`.
4. Click **Save** and wait for deployment.
5. Open the URL displayed in Settings → Pages. It will usually resemble `https://YOUR-USERNAME.github.io/two-downloads/`.

## 4. Update the page

After editing `index.html`:

```powershell
git add index.html
git commit -m "Update download links"
git push
```

GitHub Pages republishes automatically.

## 5. Enable Mac and iPhone later

- **macOS:** build a Mac package using a macOS GitHub Actions runner, test the package, then host it at a stable HTTPS URL and set `DOWNLOADS.mac`. Consider code signing and notarization for distribution. Build for Apple Silicon and/or Intel as appropriate.
- **iPhone:** the Tauri desktop build is not an iOS app. You need a separate iOS-compatible build and a distribution route such as the App Store or an eligible testing route. Set `DOWNLOADS.iphone` only once the app is actually available.

## Security

A public download page is not access control. Firebase Authentication and Realtime Database Security Rules must protect chat data. A room ID in client code is not a security boundary. Never publish private keys, service-account credentials, or private source files.
