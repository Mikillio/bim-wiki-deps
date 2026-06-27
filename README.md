# bim-wiki-deps

Zrkadlo a manifest **doplnkov** pre aplikáciu **BIM LLM Wiki** (cesta C — malá MSI +
sťahovanie na požiadanie). Stratégia: `docs/dependency-strategy.md` v hlavnom repe.

Tento repozitár je **verejný zámerne** — obsahuje len verejne dostupný open-source
softvér a jeho kontrolné súčty, a aplikácia z neho sťahuje **anonymne** (bez tokenu).

## `deps-manifest.json`

Jediný zdroj pravdy o tom, čo a odkiaľ sa dá stiahnuť. Pre každý doplnok: typ, archív,
cieľový podpriečinok, a verzie s **dvoma zdrojmi** (`official_url` = upstream,
`mirror_url` = naše GitHub Releases) + **`sha256`** (fail-closed overenie v aplikácii).

Aplikácia číta raw URL tohto súboru → verzie/hashe/URL aktualizujeme **bez nového
buildu aplikácie**.

## Zrkadlenie (GitHub Action `mirror.yml`)

Beží na GitHub infraštruktúre — netreba nič sťahovať/nahrávať ručne:

1. stiahne `official_url`,
2. zráta **SHA-256**,
3. vytvorí *Release* `<tool>-<version>` a nahrá asset,
4. doplní `mirror_url` + `sha256` do `deps-manifest.json` a commitne.

Spustenie:

```
gh workflow run mirror.yml \
  -f tool=whisper -f version=r245.4 \
  -f asset_name=Faster-Whisper-XXL_r245.4_windows.7z \
  -f upstream_url=https://github.com/Purfview/whisper-standalone-win/releases/download/Faster-Whisper-XXL/Faster-Whisper-XXL_r245.4_windows.7z
```

## Čo sa zrkadlí a čo nie

- ✅ **Binárky** (Whisper standalone, Tesseract) — sem (GitHub Release, limit 2 GB/súbor).
- ✅ **Modely** (Whisper/NaiveNeuron/embedding) — na **HuggingFace** (free, bez limitu),
  nie sem (large-v3 ~3 GB > 2 GB; HF je na modely stavaný).
- ❌ **Poppler** — GPL, len oficiálny upstream (rehosting = GPL povinnosti).
- ❌ **gemma4:31b (~20 GB)** — len Ollama register (priveľké, netreba).

Licencie: Tesseract Apache, Whisper/CTranslate2 MIT, NaiveNeuron MIT — zrkadlenie OK
s uvedením autora. Whisper standalone nesie cuDNN (NVIDIA redistribučné podmienky).
