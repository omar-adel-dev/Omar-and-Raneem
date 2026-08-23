# Omar & Raneem — Wedding Invitation Website

A responsive, bilingual (English/Arabic) wedding invitation website with a live countdown, venue map, photo gallery, RSVP form, and welcome music.

## Structure

```
wedding-invitation/
├── index.html      # Everything — markup, styling, and script all in one file
├── song.mp3        # Background music
└── photo-01.jpg …  # Gallery photos (photo-01.jpg through photo-25.jpg)
```

Everything (CSS and JavaScript) is inlined directly into `index.html`, on purpose — it means the page always displays correctly no matter how it's opened (double-clicked locally, previewed in a file manager, dragged into a browser), since there's nothing external for it to fail to find. Photos and the song sit right alongside `index.html` in the same folder — no subfolders — because that's the flat structure GitHub Pages ended up serving this from.

## 1. Preview it locally

Just double-click `index.html`, or drag it into any browser. No server, no build step needed.

## 2. Connect the RSVP form (Formspree)

1. Go to [formspree.io](https://formspree.io) and create a free account.
2. Create a new form and copy your form ID (looks like `xayzabcd`).
3. In `index.html`, find this line:
   ```html
   <form id="rsvp-form" class="rsvp-form" action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
   ```
4. Replace `YOUR_FORM_ID` with your real ID.
5. Submit a test RSVP — responses will show up in your Formspree dashboard and get emailed to you.

Until you do this, the form will show a friendly "not connected yet" message instead of failing silently.

## 3. Add your photos

Drop your image files into the same folder as `index.html` (no subfolder), named `photo-01.jpg`, `photo-02.jpg`, etc.

In `index.html`, find the gallery section (search for `id="gallery-track"`) — each photo is one line:

```html
<div class="gallery-item"><img src="photo-01.jpg" alt="Omar and Raneem" loading="lazy"></div>
```

Add or remove lines to match how many photos you have, keeping the filenames in sync. The gallery scrolls automatically (an infinite-loop animation, forced left-to-right in both languages so it doesn't break under Arabic's right-to-left layout) — no other setup needed.

## 4. Add your song

Drop your audio file into the same folder as `index.html` and name it `song.mp3` (or update the `src` in the `<audio id="bg-music">` tag in `index.html` to match your filename).

Guests will see a "Tap to Enter" welcome screen — this is required because browsers block websites from autoplaying sound before any interaction. Once tapped, the song plays and loops; a small music-note button (top corner — left in English, right in Arabic) lets guests mute/unmute.

Make sure you have the right to use the song (a track you own, a royalty-free track, or one you've licensed) since the site may be shared publicly.

## 5. Customize details

Search `index.html` for these values and adjust as needed:

- Date/time: `October 31, 2026`, `2:00 PM – 6:00 PM`
- Venue: `Tia Vie Venue` and the Google Maps link
- Dress code note
- RSVP deadline: `October 10, 2026`
- Countdown target: in `index.html`'s `<script>` tag, the line `var WEDDING_DATE = new Date(2026, 9, 31, 14, 0, 0);` (month is 0-indexed, so `9` = October)

All English/Arabic text lives in the `translations` object inside the `<script>` tag near the bottom of `index.html` — edit both language blocks to keep them in sync.

## 6. Deploy it

Easiest free option: **GitHub Pages**.

1. Push this folder to a GitHub repository.
2. In the repo settings, go to Pages → set the source to your main branch.
3. Your site will be live at `https://<username>.github.io/<repo-name>/`.

Other free options: Netlify or Vercel (drag-and-drop the folder, or connect the repo).

## Notes on privacy

If you plan to make the GitHub repository public, keep in mind the RSVP form action, guest names typed into the form, and any personal venue details will be visible in the source code and commit history. Consider keeping the repo private, or using environment-specific config if you want the code public but the real event details private.
