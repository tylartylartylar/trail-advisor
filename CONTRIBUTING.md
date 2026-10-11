# Contributing

Thanks for helping improve Trail Advisor. This is an early portfolio demo, so changes should favor clear provenance, low operational overhead, and careful safety wording.

## Development

1. Fork the repository or create a short-lived branch from `alpha`.
2. Keep pages static unless a documented product need justifies a build tool or backend.
3. For new public data, include its authoritative source, terms/license, attribution, freshness, geographic coverage, request limits, and any required user-facing caveat in `docs/data-sources.md` and the UI.
4. Do not infer a trail is open or safe from its presence in a dataset. Do not send or log precise location/search history without a reviewed privacy design.
5. Test keyboard use, focus visibility, reduced motion, contrast in light/dark/red modes, mobile layout, empty states, and provider failures.
6. Open a pull request against `alpha` with a concise summary, screenshots for visual changes, checks performed, and data/license notes. A maintainer reviews changes before `alpha` is promoted to `main`.

## Branches and releases

- `main` is the Pages-published portfolio branch.
- `alpha` is the pre-release integration branch.
- Use short-lived feature branches for substantial work; do not commit directly to `main`.
- Use semantic pre-release tags such as `v0.1.0-alpha.1`. A tag identifies a review milestone; it does not imply production readiness.
- Promote a reviewed alpha to `main` with a pull request. The Pages workflow deploys the resulting main commit.

## Change checklist

- [ ] Source/terms and UI attribution documented for data changes.
- [ ] Page remains usable with keyboard and reduced-motion settings.
- [ ] Search, loading, empty, and error states remain understandable.
- [ ] No API keys, user coordinates, or secrets added to the repository.
- [ ] README and architecture docs reflect any changed behavior.
