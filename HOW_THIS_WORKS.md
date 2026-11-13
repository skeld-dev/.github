# How the Skeld organization profile works

GitHub displays `profile/README.md` from the public `skeld-dev/.github` repository on the organization's overview page. The README embeds SVG cards served by a dedicated Cloudflare Worker, `skeld-gh`. The Worker and preview tools live in the local `custom-profile/` directory, which is excluded from this public repository. This mirrors the layout of the ul0gic personal profile.

## Local layout

```text
skeld-github/
  profile/README.md             public organization profile
  custom-profile/               local card project, excluded from this repository
    src/cards/                  header and contract diagram
    src/lib/                    SVG helpers and Polar theme
    src/registry.ts             shared card routes
    src/worker.ts               Worker request handling
    src/preview.ts              local image preview
    public/assets/              optimized artwork, font and font license
    source-assets/              unchanged original PNGs
    wrangler.jsonc              independent skeld-gh Worker
```

The Skeld framework and website are maintained in a separate checkout. This profile does not import or deploy them.

## Preview and deploy

From `custom-profile/`:

```sh
npm install
npm run dev
npm run check
npm run lint
npm run build
npm run worker:dev
npm run worker:deploy
```

Vite serves the gallery on port 5181. The local Worker serves port 8788. Both bind to all network interfaces with no need to alter the website's development server.

Deployment requires separately configured Cloudflare credentials. No credentials, account email or tokens belong in the source or public README. This Worker needs no GitHub token, database or live statistics fetch. Its content describes implemented framework behavior rather than displaying sample metrics.

## Images on GitHub

The Worker serves `/header`, `/header-mobile`, `/contract` and `/contract-mobile` as `image/svg+xml`. Each SVG embeds its own artwork and font because images embedded in a README cannot depend on external resources loaded from within the SVG. The original PNG artwork is retained locally; smaller WebP delivery copies preserve the design. Plus Jakarta Sans is accompanied by its OFL notice in `/assets/plus-jakarta-sans-OFL.txt`.

The README's `picture` elements select the stacked mobile layouts below 640px. Alt text describes the cards, and ordinary Markdown carries the main product facts. The contract diagram's animation runs once and is disabled under `prefers-reduced-motion`.

Cloudflare and GitHub's image proxy cache responses. When changing a card, increment the README image query version to request a fresh image. Recheck the public organization page after publishing, including mobile picture sources.

`/icon.png` serves a 460px transparent PNG prepared for GitHub's organization avatar upload. GitHub's organization settings handle the avatar separately from the profile README.
