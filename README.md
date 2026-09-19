# Photo Frame Fitter

Everything is in one file, `index.html`. It needs no build step and makes no network requests.

## Windows (Edge or Chrome)
Double-click `index.html`. It works offline.

### Sony RAW (.ARW)
The Windows version opens uncompressed Sony ARW files (such as those from the a7 II) at full sensor resolution:

- **Colors:** it uses the camera's white balance and a standard color profile. Colors come out close to the camera's JPEG but not identical.
- **Not applied:** lens corrections and noise reduction.
- **Not supported:** compressed ARWs, other RAW formats, and ARWs on iPhone.
- **Speed:** each photo takes a few seconds to save. Big batches are downloaded as ZIP parts of up to 2 GB each. Chrome or Edge may ask once to allow multiple downloads.

## iPhone (Safari)
The file must be hosted, because iPhone Safari won't run a page opened from the Files app. Either:

- **Netlify Drop:** open https://app.netlify.com/drop and drag this folder onto the page. You get a URL.
- **GitHub Pages:** push this folder to a repo, then turn on Settings → Pages (branch `main`, folder `/`).

It is hosted on GitHub Pages at <https://sheltonsamuele-hue.github.io/photo-frame-fitter/>. Open that in Safari, then tap Share → **Add to Home Screen**.

A claude.ai artifact link is **not** suitable: artifact pages block downloads, so saving wouldn't work.

## Developer tests
Open `index.html#debug` (or add `?debug` to the hosted URL) and use the test panel:

- **Run synthetic tests:** renders noise images in Fit and Fill across several frame setups. For each PNG, it checks that the photo region is pixel-identical to the decoded source, that the `pHYs` DPI and the border color are correct, and that no resampling `drawImage` call happens. It also checks EXIF orientation handling, JPEG JFIF density, EXIF preservation, the canvas size limit, the ZIP writer, and the ARW decoder (using a synthetic ARW file).
- **Test loaded photos:** runs the same pixel-identity check on your own photos.
