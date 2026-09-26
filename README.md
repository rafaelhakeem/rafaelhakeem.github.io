# Adrian's Ad Island · Portfolio

This is a cartoon 3D portfolio for programmatic and performance marketing. Every building on the floating island is one real campaign, and its billboard shows the real creative. Below the island, every campaign gets its own highlight panel with a creative gallery, plus a full case study.

There is no build step. It is plain HTML with [Three.js](https://threejs.org), loaded from the jsDelivr CDN.

## What's in the folder

```
index.html                      the whole site
assets/c/<campaign>/…           creatives (webp stills + mp4 animated units)
assets/audio/                   background music (CC0)
Adrian_Rafael_Hakeem_CV.pdf     linked from the "Download CV" buttons
```

Upload the **whole folder**, including `assets/`. Without it, the images won't load.

## Put it on GitHub Pages

1. Create a public repo, for example `<your-username>.github.io`.
2. Upload everything in this folder (drag the files and the `assets` folder into **Add file → Upload files**), then commit.
3. Go to **Settings → Pages**, choose **Deploy from a branch**, select `main` and `/ (root)`, then save.
4. After about a minute the site is live.

**Note:** opening `index.html` by double-clicking it works in Chrome. For the best result, test on GitHub Pages or with a local server (`python3 -m http.server`).

## Edit settings

Search `index.html` for `const CONFIG` to set your email, LinkedIn, GitHub, CV file name and GA4 ID.

## Add or change a campaign

1. Add the campaign object to `CAMPAIGNS` (KPIs, tiles, what you did, insights, chart).
2. Put its creatives in `assets/c/<id>/` and list them under the same id in `CREATIVES`. Each entry has `p` (image or poster), an optional `v` (mp4), `cap` (caption) and the pixel size `w`/`h`.
3. Add an `EP` entry with:
   - `n`: episode number
   - `tag`: one-line hook
   - `bg`: panel colour
   - `bb`: which creative goes on the billboard
   - `e`: emoji
   - `hi`: which insight to feature
4. For a themed building, add a function with the same id to `THEMES` in the Three.js script. Without one, it uses the OLX building shape.

To convert an animated GIF creative to a small mp4:

```
ffmpeg -i creative.gif -movflags +faststart -pix_fmt yuv420p -vf "scale=trunc(min(iw\,640)/2)*2:-2" -c:v libx264 -crf 27 -an 1.mp4
```

## Background music

Two 8-bit lo-fi tracks by TAD, both released as **CC0 (public domain)** on OpenGameArt, so you can use them freely. They're credited in the footer as a courtesy.

- [Ice Cave](https://opengameart.org/content/8-bit-lofi-ice-cave)
- [Iced Village](https://opengameart.org/content/iced-village-8-bit-lofi-hip-hop)

The files are in `assets/audio/`. The music starts at a low volume after the visitor's first click or tap, then loops between the two tracks. To change the tracks or the volume, edit `CONFIG.music`.

## Fallbacks and performance

- **No WebGL, or the CDN is blocked:** a flat cartoon island is shown instead, and everything else still works. Add `?nogl` to the URL to preview this.
- **Rendering:** the island only renders while it is on screen. On slow devices it turns off shadows and then outlines.
- **Videos:** they play only while visible.
- **Reduce motion:** with this setting on, animations stop and videos show controls.

## Deep links

`#case-<id>` opens a case study directly, for example `/#case-richeese`.

## Confidentiality

Budgets, rate cards and IO numbers are left out. The creatives belong to the brands, so check with your employer and clients before publishing them. 
