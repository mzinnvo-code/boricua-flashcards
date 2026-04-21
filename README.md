# Boricua Flashcards

A mobile-friendly and desktop-friendly Spanish flash card app tuned for Puerto Rican Spanish.

## Features

- High-frequency Spanish verbs
- High-frequency everyday vocabulary
- Puerto Rico vocabulary pack and usage notes
- Study mode and quiz mode
- XP, streak, accuracy, and mastered-card tracking
- Local progress save in the browser
- Export/import progress backup
- Installable on phones as a home-screen app
- Offline support with a simple service worker

## Publish on GitHub Pages

1. Create a new public GitHub repository, for example `boricua-flashcards`.
2. Upload all files in this folder to the root of the repository.
3. In GitHub: **Settings -> Pages**
4. Under **Build and deployment**, choose **Deploy from a branch**.
5. Select **Branch: main** and **Folder: /(root)**.
6. Save.

Your site URL will usually be:

`https://mzinnvo-code.github.io/<repo-name>/`

Example:

`https://mzinnvo-code.github.io/boricua-flashcards/`

## Local development

This is a plain static web app. No build step is required.

You can open `index.html` directly in a browser, but for full install/offline behavior it is better to host it through GitHub Pages or any static web host.

## Data storage

Progress is stored locally in the browser using localStorage. Export your progress if you want a backup or plan to move devices.

## Custom domain later

When you are ready to use a custom domain, add a `CNAME` file at the repo root with your domain name and update GitHub Pages settings.
