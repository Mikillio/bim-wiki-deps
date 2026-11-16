# bim-wiki-deps

Manifest a zrkadlo súčastí, ktoré si desktopová aplikácia **BIM LLM Wiki** sťahuje
sama. Sú tu len odkazy na verejne dostupný open-source softvér, jeho kontrolné súčty
a pri zrkadlených súboroch aj samotné súbory.

## `deps-manifest.json`

Pre každú súčasť: cieľový podpriečinok a verzie so zdrojom u autora (`official_url`),
prípadne so zrkadlom v Releases tohto repozitára (`mirror_url`), plus `sha256` a `size`.

Kontrolný súčet je povinný: súbor bez `sha256` sa neinštaluje.

## Zrkadlené súbory a ich licencie

Zrkadlené súbory sú kópie vydaní ich autorov, niektoré sú len premenované.
DocumentFigureClassifier v2.5 je ten istý model prevedený do formátu ONNX; váhy sú nezmenené.
Autorstvo a licencie patria autorom.

| súčasť | autor / zdroj | licencia |
|---|---|---|
| Tesseract OCR 5.5.0 | [tesseract-ocr/tesseract](https://github.com/tesseract-ocr/tesseract) | Apache-2.0 |
| PDFium | [PDFium](https://pdfium.googlesource.com/pdfium/) · zostavenie [bblanchon/pdfium-binaries](https://github.com/bblanchon/pdfium-binaries) | BSD-3-Clause; archív obsahuje `LICENSE` a licencie pribalených knižníc v priečinku `licenses/` |
| mmarco-mMiniLMv2 | [cross-encoder/mmarco-mMiniLMv2-L12-H384-v1](https://huggingface.co/cross-encoder/mmarco-mMiniLMv2-L12-H384-v1) | Apache-2.0 |
| mDeBERTa-v3 XNLI | [MoritzLaurer/mDeBERTa-v3-base-xnli-multilingual-nli-2mil7](https://huggingface.co/MoritzLaurer/mDeBERTa-v3-base-xnli-multilingual-nli-2mil7) · ONNX export [Xenova](https://huggingface.co/Xenova/mDeBERTa-v3-base-xnli-multilingual-nli-2mil7) | MIT |
| RapidOCR (PP-OCRv6) | [RapidAI/RapidOCR](https://www.modelscope.cn/models/RapidAI/RapidOCR) · [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | Apache-2.0 |
| DocumentFigureClassifier v2.5 | [docling-project/DocumentFigureClassifier-v2.5](https://huggingface.co/docling-project/DocumentFigureClassifier-v2.5) | MIT; text licencie je v release ako LICENSE-DocumentFigureClassifier-v2.5.txt |
| PP-DocLayoutV3 | [PaddlePaddle/PP-DocLayoutV3_onnx](https://huggingface.co/PaddlePaddle/PP-DocLayoutV3_onnx) · [PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) | Apache-2.0; text licencie je v release ako LICENSE-PP-DocLayoutV3.txt |

Release obrazky-1 obsahuje aj súbor ziak.onnx, ktorý je dielom autora aplikácie a nie je pod otvorenou licenciou.

Ostatné súčasti sa sťahujú priamo od ich autorov, nie zo zrkadla. Patrí medzi ne
Poppler, ktorý je pod licenciou GPL.
