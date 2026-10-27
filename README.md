# Decoding Universe — Episode 3: Gluons

A Vite + React static website containing a silent, code-generated 15-minute science animation. It does not contain Lovable narration, music, sound effects, or external video assets. The animation is drawn procedurally by `src/renderer.js` and plays on a canvas.

## Important export behavior

- The website preview is the live animation, not a pre-rendered MP4 hosted by Vercel.
- The **Generate & download** button records the animation in the visitor's browser in real time from 00:00 to 15:00. It is not a server-side render job.
- Resolution presets are 480p, 720p, 1080p, 4K, and 8K. They are target canvas dimensions. Actual recording stability, frame rate, sharpness, and compatibility depend on the visitor's browser, operating system, GPU, available memory, and supported MediaRecorder codecs.
- The app chooses the best supported browser recording codec, preferring WebM/VP9 and then WebM/VP8, with MP4 only if the browser reports native support. It does not transcode to MP4.
- Current Chrome/Edge on desktop can use the File System Access API so recording chunks are written to the chosen file instead of being accumulated in RAM. Other browsers may use the in-memory fallback. Long 4K/8K exports can fail on underpowered systems.
- Keep the tab open and in the foreground during export; browser throttling or device load can cause dropped frames.
- For production release, test all target resolutions on the computer that will make the final video. 1080p is the best initial test.

## Run locally

Requires Node.js 20+ (Node 22 recommended).

```bash
npm install
npm run dev
```

Open the local address shown by Vite.

Build and preview the production bundle:

```bash
npm run build
npm run preview
```

## Deploy to Vercel via GitHub

1. Create a GitHub repository, for example `decoding-universe-episode-3`.
2. Upload the contents of this project folder to the repository root. Do not upload the project inside an extra nested folder.
3. In Vercel, import that GitHub repository.
4. Vercel should detect Vite. The included `vercel.json` defines the build command (`npm run build`) and output directory (`dist`).
5. Deploy. No environment variables or backend API routes are required.

## Architecture

- `src/episode.js` defines all 17 chapters and the 15-minute timeline.
- `src/renderer.js` draws the entire silent animation, labels, field visualizations, transitions, and particle scenes.
- `src/App.jsx` provides the player, timeline, chapter navigation, output-resolution selector, and client-side recording/export controls.
- `src/styles.css` contains the responsive website design.

## Scientific visualization note

The graphics are conceptual representations for education. They are not literal photographs of quarks or gluons. The proton's `uud` label refers to its valence-quark content, and the animation distinguishes fundamental QCD from residual nuclear interaction.
