# TODO

Outstanding items after the al-folio migration (site went live 2026-09-04).
Excluded from the Jekyll build, so this file is not published.

## Housekeeping (do first, cheap)

- [x] ~~`git pull` on local `main`~~ — done 2026-09-05; the checkout is current.
- [ ] **Remove the worktree and its branch.** Verified ready 2026-09-05:
      `origin/main` and `origin/worktree-al-folio-migration` are both `f7a5664`,
      `git log origin/main..origin/worktree-al-folio-migration` is empty, and the
      worktree has no uncommitted changes. Nothing is lost by deleting it.

      Order matters — the branch is checked out by the worktree, so git refuses to
      delete it until the worktree is gone:

      ```
      git worktree remove .claude/worktrees/al-folio-migration
      git branch -d worktree-al-folio-migration
      git push origin --delete worktree-al-folio-migration
      ```

      Caveat: this deletes the directory, so any editor tab open on a file under
      `.claude/worktrees/al-folio-migration/` goes stale. The same files live in
      the main checkout.

## Review

- [ ] **Look at the two generated thumbnails.** These were built without any way
      to render them, so nobody has actually seen them:
  - `/projects/sudoku/` — `assets/img/fig_sudoku_candidates.svg`
  - `/projects/path-integral-gnn/` — `assets/img/fig_path_integral_gnn.svg`

      Both are valid SVG using the same palette and dark-mode block as
      `fig_core_vs_loss.svg`, but the layout is unverified.

- [ ] **Profile photo** (`_pages/about.md`, `profile.image`) is
      `RSNA_presentation_2024.jpg` — a conference-podium shot doing headshot duty,
      because it is the only photo of Hugo in the repo.

## Polish

- [ ] **RSS stylesheet.** `/feed.xml` renders as raw XML in browsers (they all
      dropped native feed rendering). An XSL stylesheet would make it a readable
      "subscribe" page. The feed itself is correct — 8 posts, full content, 81KB.

- [ ] **Vendor the CDN assets.** Every page pulls 8 files from `cdn.jsdelivr.net`
      plus Google Fonts at runtime: fontawesome, academicons, scholar-icons
      (all the social icons), masonry-layout (the projects grid), mathjax,
      medium-zoom, imagesloaded, vanilla-back-to-top. Only `main.css` and
      `tailwind.css` are served locally. Vendoring removes the third-party
      dependency and the failure mode where a blocked CDN degrades the page.

- [ ] **Five dead images** in `assets/img/`: `Apple-Logo.png`, `whiterabbit.jpg`,
      `mckinsey.png`, `stanford-university-logo.png`, `polytechnique.jpg`. The old
      about page used them inline; al-folio's CV layout does not. Harmless but dead.

## Optional workflows (deliberately not added)

- [ ] **`copilot-setup-steps.yml`** — only if GitHub Copilot's coding agent is
      wanted on this repo. Needs `package-lock.json`, which is not present
      (`package.json` was deleted as dead al-folio dev tooling).
- [ ] **`render-cv.yml`** — auto-renders a PDF from `_data/cv.yml` via RenderCV and
      commits it back. Needs `assets/rendercv/` config plus `requirements.txt`,
      neither of which was copied. Would not replace the existing
      `assets/pdf/resume.pdf`.

## Minor prose nits in the little-lm post

Flagged and consciously skipped — "I dont really care about minor typos".

- [ ] `_posts/2026-09-04-little-lm-3-8b.md` — "the same eval loss to four decimal
      places (2.0160 vs 2.0164)". Those differ *at* the fourth decimal; should be
      three, or "to within 0.0004".
- [ ] Same file — "1 forward and 2 backwards" should be "backward".
- [ ] Same file — "neighbours" is the only British spelling against "behavior"
      elsewhere.

## Notes for future work on this repo

- Publishing is now: push to `main` → the **Deploy site** workflow builds and
  pushes to `gh-pages` → live in ~2 minutes. Pages serves `gh-pages`; do not
  point it back at `main`.
- `permalink: /:title/` in `_config.yml` is deliberate and must not change — it
  preserves every pre-migration post URL.
- `external_sources: []` is deliberate. al-folio fetches medium.com RSS at build
  time and an unrescued `Net::OpenTimeout` aborts the entire build.
- ImageMagick is required for responsive images, locally and on the runner.
