# NTU Paper Access — Chrome extension

NTU Paper Access is a lightweight Chrome extension that helps NTU students quickly access research papers through the university's remote access (RemoteXs) portal.

Clicking the extension while viewing a journal article or paywalled paper opens NTU's RemoteXs login page with the current article URL pre-filled, so you can sign in and retrieve the article using NTU institutional access with a single click.


## Key features

- One-click access: open the current tab in NTU RemoteXs for authenticated access.
- Minimal and transparent: small code footprint — the extension redirects the current page to RemoteXs with your page URL as the destination.
- No tracking: the extension does not collect or send browsing data to third parties (see Privacy below).


## 🔧 How it works

When you click the toolbar icon, the extension injects a small script into the active tab that redirects your browser to:

```
https://remotexs.ntu.edu.sg/user/login?dest=<CURRENT_PAGE_URL>
```

That URL directs you to NTU's RemoteXs login; after successful login, RemoteXs will attempt to fetch the original page (the paper) using NTU's institutional access.


## Install

### Locally (developer / testing)
1. Open Chrome and go to chrome://extensions
2. Enable **Developer mode** (top right)
3. Click **Load unpacked** and select this project's folder
4. The extension should appear in your toolbar. Click it while on a paper page to test.

## Usage
1. Browse to the research article or paywalled resource you want to access.
2. Click the NTU Paper Access toolbar icon.
3. You'll be taken to NTU RemoteXs sign-in with the article URL appended — sign in with your NTU credentials.
4. After authentication, RemoteXs will try to fetch the requested content for you.

Tip: If a redirect fails, copy the current article URL and paste it into RemoteXs manually at https://remotexs.ntu.edu.sg/user/login?dest= (append the escaped URL).

## Development & customization

- Main files:
  - `bookmarklet-code.js` — the small redirect script executed in the active tab.
  - `event.js` — service worker that injects `bookmarklet-code.js` when the extension icon is clicked.
  - `manifest.json` — extension metadata and permissions.

- Update the redirect or behavior by editing `bookmarklet-code.js`.

### Permissions

This extension requests the following minimal permissions:

- `activeTab`, `tabs`, `scripting` — to run the redirect in the current tab.
- `host_permissions: ["<all_urls>"]` — allows injecting the redirect script on the active page.

## Privacy

NTU Paper Access is intentionally simple and privacy-friendly:

- It only redirects the current tab to NTU RemoteXs and does not collect or transmit browsing history or personal data to third parties.
- No analytics or external APIs are used.

## Troubleshooting

- If clicking the extension does nothing: check chrome://extensions for runtime errors, and ensure the extension is enabled.
- If RemoteXs doesn't load your article: try copying the article URL and pasting it in the NTU library website.

## Contributing

Contributions, issues and feature requests are welcome. Please open an issue on the project repository.

## License & credits

This project is provided under the MIT License — see `LICENSE` for details.

Built from a bookmarklet-to-extension template — adapted for NTU RemoteXs access.
