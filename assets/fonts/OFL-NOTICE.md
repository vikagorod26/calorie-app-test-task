# Vendored webfonts — provenance and licence

The two families Design System v1 names in `--font-ui` and `--font-voice`
(`04-design-system/tokens-v1.md` §2.1), vendored at Stage 7b so the deliverable
renders its own typography with no network connection.

| Family | Role in the system | Files | Axes kept |
|---|---|---|---|
| **Inter** | `--font-ui` — interface and **every figure**, tabular | 7 woff2 subsets | variable `wght` (serves 400 / 500 / 600) |
| **Newsreader** | `--font-voice` — recipe names and headlines | 6 woff2 subsets (3 roman + 3 italic) | variable `wght` and `opsz` |

## Why these are vendored rather than linked

The screens previously pulled both from `fonts.googleapis.com`. A reviewer
opening the repo offline, in a private window on a slow connection, or with an
ad blocker that filters Google Fonts, would have silently fallen back to system
fonts — and the brand rule these files carry ("words are warm, figures are
exact") would have degraded with nothing on screen explaining why. The figures
are the part that matters most: Inter is what makes them tabular and aligned.

## Provenance

Downloaded from `fonts.gstatic.com` as the exact woff2 subsets Google served for
the `css2` request the screens previously linked:

```
family=Inter:wght@400;500;600
&family=Newsreader:ital,opsz,wght@0,6..72,400;0,6..72,500;1,6..72,400
&display=swap
```

`fonts.css` reproduces all 30 `@font-face` blocks from that response with local
`src` paths and **`unicode-range` preserved verbatim**, so a browser still
downloads only the subsets a page actually needs. Inter v20, Newsreader v26.

## Licence

Both families are licensed under the **SIL Open Font License, Version 1.1**,
which permits bundling and redistribution with a project, including in a
commercial one, provided the fonts are not sold on their own and the licence
travels with them.

- Inter — Copyright The Inter Project Authors (https://github.com/rsms/inter)
- Newsreader — Copyright The Newsreader Project Authors (https://github.com/productiontype/Newsreader)

Full licence text: https://openfontlicense.org/ — and in each upstream
repository above. No font file here has been modified, renamed internally, or
re-hinted; the `.woff2` bytes are Google's own subsets as served.
