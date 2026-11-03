For more details about my professional background and latest updates, feel free to visit my [LinkedIn](https://linkedin.com/in/lorenacw) profile.


## Adding a slide deck

1. In Keynote: **File → Export To → HTML…**
   Rename the exported folder to a short name, e.g. `endpoint-that-walks`,
   and put it in `assets/talks/`, so you have `assets/talks/endpoint-that-walks/index.html`.

2. Create `_talks/endpoint-that-walks.md` (same name as the folder):

   ```yaml
   ---
   title: "The Endpoint that walks"
   subtitle: "Mobile devices as physical security risks"
   event: Sikkerhetsfestivalen
   place: Lillehammer
   date: 2026-08-26
   cover: /assets/talks/endpoint-that-walks-cover.jpg   # optional thumbnail for the Talks page
   pdf: /assets/talks/endpoint-that-walks.pdf           # optional download
   ---
   Optional abstract or notes in Markdown, shown under the slides.
   ```

3. To link it from the homepage and CV, add `deck: endpoint-that-walks`
   to the matching entry in `_data/presentations.yml`.

The slides are then at `/talks/endpoint-that-walks/`, framed in the site,
with fullscreen and "open in new tab" buttons. Without a `cover`, the Talks page
shows a coloured title card instead.
