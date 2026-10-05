# Burmese Wiktionary Cleaned Lexicon

A systematically parsed, cleaned, and structured lexical dataset extracted from **Myanmar Wiktionary (`my.wiktionary.org`)**. This resource is tailored specifically for computational linguistics, corpus analysis, and Natural Language Processing (NLP) tasks targeting Burmese—a low-resource language with limited structured lexical availability.

---

## Dataset Overview & Provenance

- **Source:** Myanmar Wiktionary (`my.wiktionary.org`)
- **Data Snapshot / Dump Date:** 2026-08-01 (`mywiktionary-20260801-pages-articles.xml.bz2`)
- **Data Integrity & As-Is Fidelity:** All textual definitions, lexical entries, grammatical labels, and transliterations directly mirror the source content in `my.wiktionary.org` as of the snapshot date. No synthetic definitions or lexical alterations were introduced; processing was strictly constrained to structural extraction, Wikitext markup stripping, HTML artifact normalization, and relational schema normalization.
- **License:** Distributed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** license. Users are free to share, adapt, transform, and build upon this material for any purpose, including commercial applications, provided appropriate attribution is given.

---

## Technical Architecture & Schema

Each entry in the dataset represents a distinct **Word–POS tuple**. Words containing multiple parts of speech are split into individual, discrete rows to ensure clean downstream classification labels.

### Data Fields

| Field | Type | Description |
|:---|:---|:---|
| `word` | `string` | Primary Burmese headword (lexical entry) in Unicode. |
| `mlcts` | `string` | Standard MLC (Myanmar Language Commission) Transcription System Romanization. Complete (100%) coverage across all records. |
| `ipa` | `string` or `null` | International Phonetic Alphabet representation, when available in the raw entry. |
| `pos` | `string` | Myanmar grammatical category / Part of Speech (e.g., နာမ်, ကြိယာ, နာမဝိသေသန). |
| `definitions` | `list[string]` | Array of clean dictionary definitions stripped of Wiki markups, links, and HTML entities. |
| `classifier` | `string` or `null` | Numerical classifier associated with the entity. Grammatically constrained strictly to entities where `pos == "နာမ်"` (Nouns). Set to `null` for all other syntactic classes. |

---

## HuggingFace Link

🤗 Huggingface - https://huggingface.co/datasets/its-autumn/burmese-wiktionary

---

## Dataset Summary & Statistics

### Corpus Metrics

| Metric | Count |
|:---|---:|
| **Total Cleaned Records** | 22,191 |
| **Unique Headwords (Words)** | 20,759 |
| **Total Definitions** | 28,402 |
| **Avg. Definitions per Record** | 1.28 |
| **Avg. Definition Length** | 42.0 characters |
| **Max Definitions on a Single Word** | 29 (ထိုး) |

### Part of Speech (POS) Distribution

| Part of Speech (POS) | Count | Percentage |
|:---|---:|---:|
| **နာမ် (Noun)** | 12,878 | 58.03% |
| **ကြိယာ (Verb)** | 7,845 | 35.35% |
| **နာမဝိသေသန (Adjective)** | 907 | 4.09% |
| **ဝါစင်္ဂ (Particle / Functional)** | 375 | 1.69% |
| **သမ္ဗန္ဓ (Conjunction)** | 107 | 0.48% |
| **ဝိဘတ် (Postposition)** | 61 | 0.27% |
| **အာမေဍိတ် (Interjection)** | 15 | 0.07% |
| **ပစ္စည်း (Affix / Enclitic)** | 3 | 0.01% |

### Metadata Field Coverage

| Field | Available Count | Coverage (%) | Description / Constraints |
|:---|---:|---:|:---|
| `word` | 22,191 | 100.00% | Primary lexical headword |
| `mlcts` | 22,191 | 100.00% | Standard MLC Romanization |
| `definitions` | 22,190 | 100.00% | Clean, normalized definitions list |
| `classifier` | 7,821 | 35.24% | Syntactically constrained to Nouns only |
| `ipa` | 113 | 0.51% | IPA pronunciation phonetic strings |

---

## Intended Use Cases

- **Part-of-Speech (POS) Tagging & Parsing:** Provides high-density lexical ground truth for training sequence-labeling models (CRFs, BiLSTM-CRF, Transformer-based taggers).
- **Noun-Classifier Semantics:** Benchmark dataset for evaluating lexical dependency and noun-to-classifier selection tasks in Burmese.
- **Grapheme-to-Phoneme (G2P) & Transcription:** High-coverage parallel corpus for training grapheme-to-MLCTS transliteration engines.
- **Lexical Sense Disambiguation & Tokenization:** Grounding dictionary entries for word boundary disambiguation and dictionary-based segmenters.

---

## Acknowledgements & Technical Credits

Special thanks to **[Khant Sint Heinn (Kalix Louis)](https://huggingface.co/kalixlouiis)** [@kalixlouiis](https://github.com/kalixlouiis) for technical assistance and engineering contributions toward developing the extraction scripts, streaming parsers, and data cleaning workflows used in this project.

---

## Citation & Attribution

If you utilize this dataset in research, tool development, or technical benchmarking, please attribute it as follows:

```bibtex
@dataset{burmese_wiktionary_lexicon_2026,
  author       = {Autumn and Khant Sint Heinn},
  title        = {Burmese Wiktionary Cleaned Lexicon},
  year         = {2026},
  publisher    = {Hugging Face},
  howpublished = {https://huggingface.co/datasets/its-autumn/burmese-wiktionary},
  note         = {Extracted and normalized from Myanmar Wiktionary dump dated 2026-08-01 under CC BY 4.0}
}
```
