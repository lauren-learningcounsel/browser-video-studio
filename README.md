# Browser Video Studio

A static, browser-only video production application. No backend, account, paid API, or local installation is required to run it from an HTTPS static host.

## Included
- MP4/MOV draft intake and validation using browser decode + FFmpeg.wasm probe
- Request metadata and first-4-MB SHA-256 fingerprint
- Technical stream details and silence detection
- Optional Whisper Tiny English transcription in-browser via Transformers.js
- XLSX Recommended Edits workbook
- Human selection and approval before editing
- Optional music-bed mix
- FFmpeg.wasm MP4 render and browser playback validation
- Synthetic self-test (creates synthetic video in memory only)

## Privacy
Draft videos and added audio assets are read into browser memory and are not uploaded to an application server. The application does not write media to IndexedDB or remote storage. CDN requests fetch application libraries and model files only. The optional transcription model is downloaded from Hugging Face; the selected media remains local to the browser. Closing the tab releases app-held object URLs and in-memory data; browser download copies remain wherever the user saved them.

## Run / deploy
Serve this folder as static files over HTTPS. `index.html` is the entry point. It uses public CDN modules for FFmpeg.wasm, Transformers.js and SheetJS. No build step is required.

## Known limitations
- Browser-only FFmpeg is much slower and more memory constrained than native FFmpeg.
- This implementation has not been published to a public host yet. A GitHub connection is needed to publish to the user's account.
- MOV/MP4 codec support depends on the bundled FFmpeg build and browser.
- Silence detection is a measurable heuristic, not semantic editing.
- Whisper Tiny English is English-focused; accuracy varies and long recordings can take substantial time.
- The current editor's music-bed support uses the first selected audio asset, loops it, and mixes it under the draft.
- One source video/audio stream is supported; complex multi-camera editing, speaker diarization, cloud-drive intake and Zoom cloud download are not implemented.
- The self-test checks synthetic capture, WASM render and output decode. It does not test every device/browser or every media codec.