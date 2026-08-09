# palitext — remote corpora for Palitext

Public distribution of optional Pāli corpora for the Palitext iOS/macOS app:

1. **Zhuang Chunjiang extras** — Khuddaka and related books as `{ID}.sqlite.zip` (Release `v1`)
2. **PTS Tipiṭaka TOC** — bilingual outline at [`pts/pts_toc.json`](pts/pts_toc.json)

## App endpoints

| Resource | URL |
|----------|-----|
| Manifest | https://raw.githubusercontent.com/yrekniht7/palitext/main/remote_manifest.json |
| Release assets | https://github.com/yrekniht7/palitext/releases/download/v1/ |

`remote_manifest.json` uses `baseURL` + `downloadPath`, with `sha256` / `byteSize` for install verification.

## Layout

```
remote_manifest.json   # catalog for App downloads
pts/pts_toc.json       # Tipiṭaka / Aṭṭhakathā / Tīkā / Anya bilingual TOC
NOTICE.md              # license boundaries (Zhuang vs PTS)
LICENSE                # CC0 for this repo's own metadata/docs only
```

Large `.sqlite.zip` files are **GitHub Release** assets only (not in git history).

## Release `v1` packages (Zhuang extras)

All 16 collections crawl successfully from [agama.buddhason.org](https://agama.buddhason.org) folder layout (`Ud`, `It`, `Ps`, `Ni`, `Kh`, `Dh`, `Su`, `Vi`, `Pv`, `Th`, `Ti`, `Ap`, `Bv`, `Cp`, `Ja`, `Mi`):

| id | title |
|----|--------|
| Ud | 优陀那 |
| It | 如是语 |
| Ps | 无碍解道 |
| Nidd | 义释 |
| Khp | 小诵 |
| Dhp | 法句 |
| Snp | 经集 |
| Vv | 天宫事 |
| Pv | 饿鬼事 |
| Th | 长老偈 |
| Thi | 长老尼偈 |
| Ap | 阿波陀那 |
| Bv | 觉种性 |
| Cp | 所行藏 |
| Ja | 本生 |
| Mil | 弥兰陀问经 |

## PTS

- TOC is published under `pts/pts_toc.json` (first milestone).
- PTS body sqlite zips (`kind: "pts"`) may be added to later Release assets; until then the App shows TOC browse-only for leaves without a matching package.

## Release `v1` packages (PTS roots)

Four first-level CSCD Tipiṭaka packages (Pāli only):

| id | title | approx zip |
|----|--------|------------|
| pts-mula | 三藏（根本） / Tipiṭaka (Mūla) | ~10 MB |
| pts-atthakatha | 义注 / Aṭṭhakathā | ~21 MB |
| pts-tika | 疏钞 / Tīkā | ~19 MB |
| pts-anya | 其他 / Anya | ~10 MB |

Source: [siongui/data](https://github.com/siongui/data) `tipitaka/romn/cscd`. See NOTICE.md.

## Licenses

See [NOTICE.md](NOTICE.md). Zhuang packages remain **CC BY-NC-SA 4.0**. Do not assume CC0 applies to those texts.

## Rebuild (publisher)

From the Palitext app repo:

```bash
cd Tools/Corpus
python3 build_corpus.py Ud It Dhp … --workers 6
python3 publish_remote_manifest.py \
  --ids Ud It Ps Nidd Khp Dhp Snp Vv Pv Th Thi Ap Bv Cp Ja Mil \
  --base-url https://github.com/yrekniht7/palitext/releases/download/v1/ \
  --out /path/to/this/repo/remote_manifest.json
```

Then upload zips to Release `v1` and push the updated manifest to `main`.
