# NutriScan — Vercel deployment

## What changed
- The live camera now runs in the visitor's browser with `navigator.mediaDevices.getUserMedia()`.
- Frame capture and label cropping remain client-side; the selected image is uploaded to the existing `/scan` endpoint.
- The server no longer tries to open a physical webcam or expose an MJPEG `/video_feed` route.
- `GROQ_API_KEY` is read from the environment and must be configured in Vercel.

## Deploy
1. Put `app.py`, `requirements.txt`, `vercel.json`, and `.gitignore` in the root of your GitHub repository.
2. In Vercel, import that repository.
3. In Project Settings → Environment Variables, add `GROQ_API_KEY` with your Groq key. Do not put the key in source code or commit it to GitHub.
4. Redeploy after adding/updating the environment variable.
5. Open the deployed site in a browser and allow camera access when prompted.

## Camera notes
- Browser camera access works on HTTPS (Vercel provides HTTPS) or localhost during local development.
- On a phone, use a current Safari/Chrome browser and allow camera permission. The page requests the rear camera when available.
- The camera is the visitor's device camera, not a camera attached to Vercel's server.

## OCR note
The existing Tesseract OCR fallback requires the native Tesseract executable. Vercel's standard Python runtime does not automatically include it. Groq vision analysis remains the primary scan path. If Groq is unavailable and OCR fallback is needed in production, use a hosted OCR service or configure a deployment that includes the Tesseract binary.
