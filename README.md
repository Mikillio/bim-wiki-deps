# bim-wiki-deps

Manifest a zrkadlo **voliteľných doplnkov** pre desktopovú aplikáciu
**BIM LLM Wiki**. Aplikácia si doplnky sťahuje **na požiadanie** a **anonymne**
(bez tokenu), preto je repozitár verejný.

Sú tu len odkazy na verejne dostupný open-source softvér, jeho kontrolné súčty
a — pri zrkadlených artefaktoch — samotné súbory.

## `deps-manifest.json`

Pre každý doplnok: typ, cieľový podpriečinok a verzie s **dvoma zdrojmi** —
`official_url` (upstream) a `mirror_url` (naše GitHub Releases) — plus
**`sha256`** a `size`.

Overenie kontrolného súčtu je **fail-closed**: prázdny `sha256` znamená
*neinštalovať*, nie *nainštalovať bez overenia*.

Aplikácia číta raw URL tohto súboru, takže verzie, hashe a URL sa dajú
aktualizovať bez nového buildu.

## Zrkadlenie (GitHub Action `mirror.yml`)

Stiahne upstream asset, zráta SHA-256, vytvorí *Release* `<tool>-<version>`,
nahrá asset a doplní `mirror_url` + `sha256` do manifestu.

```
gh workflow run mirror.yml \
  -f tool=whisper -f version=r245.4 \
  -f asset_name=Faster-Whisper-XXL_r245.4_windows.7z \
  -f upstream_url=https://github.com/Purfview/whisper-standalone-win/releases/download/Faster-Whisper-XXL/Faster-Whisper-XXL_r245.4_windows.7z
```

## Čo sa zrkadlí a čo nie

| | |
|---|---|
| ✅ binárky a ONNX modely | GitHub Releases (limit 2 GB na súbor) |
| ✅ veľké modely | Hugging Face |
| ❌ **Poppler** | GPL — sťahuje sa výhradne z jeho vlastnej distribúcie |
| ❌ balíky z PyPI a modely z Ollama registra | sťahujú sa priamo z ich zdrojov |

## Licencie zrkadlených artefaktov

| artefakt | upstream | licencia |
|---|---|---|
| Faster-Whisper XXL (standalone) | [Purfview/whisper-standalone-win](https://github.com/Purfview/whisper-standalone-win) | MIT (Faster-Whisper, CTranslate2); obsahuje cuDNN podľa redistribučných podmienok NVIDIA |
| Tesseract OCR 5.5.0 | [tesseract-ocr/tesseract](https://github.com/tesseract-ocr/tesseract) | Apache-2.0 |
| ONNX cross-encoder | [cross-encoder/mmarco-mMiniLMv2-L12-H384-v1](https://huggingface.co/cross-encoder/mmarco-mMiniLMv2-L12-H384-v1) | Apache-2.0 |
| ONNX NLI model | [MoritzLaurer/mDeBERTa-v3-base-xnli-multilingual-nli-2mil7](https://huggingface.co/MoritzLaurer/mDeBERTa-v3-base-xnli-multilingual-nli-2mil7) · ONNX export [Xenova](https://huggingface.co/Xenova/mDeBERTa-v3-base-xnli-multilingual-nli-2mil7) | MIT |

Zrkadlené súbory sú nezmenené kópie upstream artefaktov (pri ONNX modeloch
premenované na `model.onnx` / `tokenizer.json`). Autorstvo a licencie patria ich
autorom.
