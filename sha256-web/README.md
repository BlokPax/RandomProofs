# SHA-256 Hash Generator Web App

This folder contains a small single page application that lets you compute the
SHA-256 hash of any text. It can be served via GitHub Pages.

## Usage

1. Navigate to the `sha256-web` directory in your browser once the repository is
   hosted on GitHub Pages: `https://<username>.github.io/RandomProofs/sha256-web/`
2. Enter any text in the input box and press **Hash It**.
3. The resulting hash will appear below the form. Each result is kept so you can
   review multiple inputs.

The app uses the browser's `crypto.subtle.digest` API and does not require any
server-side code.
