# PR preview deployments

This repo uses GitHub Actions (`.github/workflows/preview.yml`) to build a
Hugo preview of every pull request and publish it to this repo's own
GitHub Pages project site, under `/pr-preview/pr-<N>/`.

Preview URL pattern:

```
https://<owner>.github.io/<repo>/pr-preview/pr-<N>/
```

For this repo that is:

```
https://angryalbatross.github.io/tdh-website/pr-preview/pr-<N>/
```

The PR Preview Action (`rossjrw/pr-preview-action`) posts a sticky comment
on each PR with that exact link and auto-removes the preview folder when
the PR is closed or merged.

## Production is on Netlify

Production (`tdhort.com`) is served by **Netlify**, connected to this
repo. Netlify watches the `master` branch and publishes the site
automatically when `master` is updated — nothing in the preview
workflow touches production.

The preview workflow:

- Never writes a `CNAME` into the preview output (it explicitly deletes
  any that ends up there), so the preview Pages site cannot claim the
  production domain.
- Deploys only to the `gh-pages` branch of *this* repo.
- Uses the project Pages URL (`<owner>.github.io/<repo>/...`) for
  `baseURL`, so preview assets resolve locally inside the preview path
  and never point at production.

## One-time setup

The first time you enable this, you need to do two things in the GitHub
UI for this repo:

1. Open the first PR that includes `.github/workflows/preview.yml`. On
   the first run, the workflow will create a `gh-pages` branch.
2. Go to **Settings → Pages** and set:
   - **Source:** Deploy from a branch
   - **Branch:** `gh-pages` / `/ (root)`
   - Leave **Custom domain** empty on this repo (the custom domain stays
     on whichever repo currently serves production through CloudFront).
3. Save. Within a minute the project Pages URL above will start serving
   any `pr-preview/pr-<N>/` folders that exist on `gh-pages`.

After that, every PR automatically gets a preview URL and a sticky
comment. Closing/merging a PR removes the preview folder.

## Notes & caveats

- Preview deploys will only run for PRs **from branches in this repo**,
  not from forks, because forks cannot push to `gh-pages` without extra
  setup. (This is the standard behavior of `rossjrw/pr-preview-action`.)
- The gallery lightbox, form submission, and Font Awesome all load via
  HTTPS CDNs, so they'll work identically on preview and production.
- The Formspree endpoint on `/contact/` will send real emails even from
  preview URLs. If you want preview form submissions to be rejected or
  silenced, swap the `action=` attribute in the form to a no-op during
  preview builds — happy to add that if desired.
