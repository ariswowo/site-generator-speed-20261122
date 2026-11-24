# Site Generator Speed — a faster drop-in for makefun-site 1.0.0

[![make.fun](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/ariswowo/site-generator-speed-20261122/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/ariswowo/site-generator-speed-20261122/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)

A faster drop-in for make.fun's own static site generator, makefun-site
1.0.0, written for the
[site-generator-speed-01-run-20261122](https://make.fun/bounty/site-generator-speed-01-run-20261122)
bounty on [make.fun](https://make.fun).

`solve.js` exports `run(input)`, which returns exactly the answer
makefun-site 1.0.0 returns for one case's input: the output tree of the
site's build, byte for byte. `main.ts` is the driver the harness runs: it
reads every case from `/input/cases.json`, answers each with `run`, and
writes `/output/answers.json`.

## How it is faster

The reference is reimplemented, not wrapped, with the same output:

- HTML escaping in one call per plain run, instead of one call per
  character.
- Slugs cached (tag names and titles repeat across a site) with a fast
  path for pure ASCII.
- Markdown rendered in a single pass over the lines, with no token
  objects.
- Words counted by a manual scan instead of a match array.
- Template loops reuse one scope object and one loop record per loop.
- Each post's card is computed once and reused by its layout.

## Files

- `main.ts` — the driver the harness runs.
- `solve.js` — the fast implementation (dependency-free ES module).
- `package.json` — marks the package as an ES module.
- `LICENSE` — MIT.

## License

MIT. See [LICENSE](LICENSE).
