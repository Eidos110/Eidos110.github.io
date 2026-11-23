# Self-hosted fonts

Both fonts are variable fonts licensed under the SIL Open Font License 1.1. The
license texts sit next to the font files.

- `fraunces-latin.woff2` — Fraunces with the `opsz` and `wght` axes; `SOFT` and
  `WONK` pinned at their defaults; weight range 400–700.
- `inter-latin.woff2` — Inter with the `wght` axis; weight range 400–700.

The files are subset to the site's copy plus Latin-1, general punctuation,
currency, trademark, arrows, and minus. Regenerate them if the copy or the
weights in `assets/css/styles.css` change. The upstream files are the Fontsource
Latin variable WOFF2 releases.

```powershell
python -m fontTools.varLib.instancer fraunces-upstream.woff2 wght=400:700 SOFT=0 WONK=1 --output=fraunces-inst.woff2
python -m fontTools.subset fraunces-inst.woff2 --flavor=woff2 --layout-features='*' `
  --unicodes='U+0000-00FF,U+2000-206F,U+20AC,U+2122,U+2190-2199,U+2212' `
  --output-file=assets/fonts/fraunces-latin.woff2

python -m fontTools.varLib.instancer inter-upstream.woff2 wght=400:700 --output=inter-inst.woff2
python -m fontTools.subset inter-inst.woff2 --flavor=woff2 --layout-features='*' `
  --unicodes='U+0000-00FF,U+2000-206F,U+20AC,U+2122,U+2190-2199,U+2212' `
  --output-file=assets/fonts/inter-latin.woff2
```

Requires `fonttools` and `brotli` (`pip install fonttools brotli`). Keep the
`@font-face` `font-weight` descriptors in sync with the instanced range.
