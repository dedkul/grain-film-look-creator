# GRAIN — Film Look Studio


A simple web-based film look creator for photos, built as a vibe-coding side project.

GRAIN runs entirely in the browser. You drop in a photo, pick a film stock preset like Kodak Portra 400 or Ilford HP5, and get back a version with that look applied. You can also tune individual sliders for exposure, contrast, grain, vignette and more.

It's inspired by tools like Dehancer and the film-look plugins in Lightroom, but stripped down to something casual and approachable. No accounts, no upload servers, no installs — just a single HTML page.

---

## How This Was Built

This project was mainly an excuse to keep practicing **vibe coding** — designing and building by talking through ideas with AI rather than writing every line by hand. I'm a designer first, not an engineer, so the goal was to get from "wouldn't this be cool" to a working tool I could actually share with friends.

Here's roughly how it came together:

1. **Started with a vague idea** — I wanted a free, online version of something Dehancer-like that anyone could use without paying or installing Photoshop.
2. **Built it one HTML file at a time** — the entire thing is a single `index.html` with embedded CSS and JavaScript. No build step, no framework, no dependencies. This was deliberate so I could iterate fast and so anyone could open the file and see exactly what it does.
3. **Let the design lead the engineering** — I started with the retro analog UI vibe (cream, brown, orange palette, monospace type, sprocket holes in the footer) and worked backwards into figuring out how to do canvas image processing.
4. **Iterated through a lot of small versions** — uploading images, getting presets to look right, fixing weird canvas rendering bugs, redoing the mobile layout when it didn't feel right, removing things that weren't working (RIP halation slider).
5. **Published it on GitHub Pages** so I could share a link and have friends actually try it.

The whole project is a deliberately small, designer-led experiment. It's not trying to compete with real film emulation tools — it's trying to be fun, easy to use, and actually useful for casual edits.

---

## What GRAIN Does

You open it, drop in a photo, and start playing.

* **Film Stock presets** — 10 looks ranging from soft warm Kodak Portra to high-contrast Tri-X to neon-night Cinestill 800T. Each preset is just a bundle of slider values that gives the photo a particular character.
* **Strength slider per preset** — every preset has its own strength dial so you can apply a Portra look at 60% if 100% feels too strong.
* **Tone controls** — exposure, contrast, highlights, shadows, saturation, temperature. Each one has a slider and a number input. Double-click any slider to reset it.
* **Film controls** — grain, bloom, vignette. Same drill.
* **Before/After toggle** so you can see how far you've come.
* **Zoom in/out** for checking detail.
* **Open Photo** to swap in a different image without losing your settings.

On mobile, all the controls live in a bottom sheet that slides up over the photo. There's also a focus mode — when you start dragging a slider, everything else fades to black so you can see only the image and the value you're changing. Inspired by Lightroom Mobile's editing flow.

---

## Why I Made It

A few reasons:

* I love the look of film photography but never carry a real film camera around.
* Most film-look plugins cost money or require Photoshop / Lightroom Classic.
* I wanted a project I could actually finish over a weekend or two, not a giant production app.
* Vibe coding is genuinely fun and I wanted to keep practicing it.

Mostly it just started from "I wonder if this would work in the browser?" and went from there.

---

## How It Works (the casual version)

Without going too deep:

* When you upload a photo, it gets drawn onto a hidden HTML `<canvas>` element.
* When you move a slider, the app reads every pixel of that photo, runs a bunch of math on the red/green/blue values, and draws the result back to a second canvas on top.
* Presets are just lists of slider values. Clicking one populates all the sliders with those values.
* Grain is added by nudging each pixel's brightness up or down by a random amount, scaled by how dark the pixel is (so grain is heavier in shadows like real film).
* Bloom is created by shrinking the image to a tiny canvas, then drawing it back at full size with "screen" blend mode — the upscaling adds a soft glow.
* Vignette is a radial gradient drawn on top.

Everything happens in your browser. The image never leaves your computer. There's no server, no upload, no tracking.

---

## What I Couldn't Get Working (and Why)

A real film look has something called **halation** — that warm red-orange glow you sometimes see bleeding from bright lights in film photos. It's caused by light bouncing off the back of the film and re-exposing the emulsion. I tried multiple times to add a halation slider, but doing it well in plain HTML/canvas turns out to be really hard — proper halation needs GPU shaders and physics-style light simulation, which is a whole different project.

So for now, halation is on the cutting room floor. The other film effects (grain, bloom, vignette) are still here and working.

---

## Tech Used

* **HTML, CSS, JavaScript** — just the basics, no frameworks
* **Canvas 2D API** — for all the image processing
* **Google Fonts** — Playfair Display, Courier Prime, Space Mono
* **GitHub Pages** — for hosting

That's literally it. One HTML file. No npm, no build, no dependencies.

---

## Try It

[**Live Demo →**](https://dedkul.github.io/grain-film-look-creator/)

Or clone the repo and just open `index.html` in a browser. There's nothing else to install.

---

## Possible Next Steps

Some things I might try later:

* Adding more film presets (Cinestill 50D, Lomo, etc.)
* A proper halation effect (would probably mean rewriting the rendering with WebGL)
* Light leak overlays
* A drag-to-compare wipe instead of a button toggle
* Saving custom user presets locally
* Better mobile gesture support

---

## Notes For Visitors

If you're a developer: this is a single HTML file with embedded CSS and JS. The image processing is pure canvas 2D pixel manipulation. There's no clever trick — just a bunch of math applied per-pixel with some debouncing to keep it responsive.

If you're a designer: this is a project I made with no real prior coding experience in canvas image processing. I figured most of it out by experimenting, breaking things, and asking AI a lot of questions. You can absolutely make small useful tools without being a "real engineer."

---

*Built by a designer who wanted a simple film-look tool and decided to vibe code one over a weekend.*
