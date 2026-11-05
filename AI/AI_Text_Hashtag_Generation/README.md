# Text & Hashtag Generation

**AD GENERATOR AI — Shared AI Module**

This module contains the notebooks and training dataset for the project's **English and Arabic marketing text and hashtag generation** workflows. It is a **joint contribution by two team members**; contributor names and GitHub profiles should be added once confirmed.

## Overview

The application prepares three marketing post types for a product and selected platform:

- **Product-Focused** — emphasizes product details and selling points.
- **Lifestyle-Focused** — frames the product in a relatable lifestyle context.
- **Campaign-Focused** — emphasizes promotions and campaign messaging.

The English and Arabic workflows are separate, and their technical approaches differ.

## Module contents

| Path | What it contains |
| --- | --- |
| `english/T5_English_3Variants.ipynb` | English **T5-Small full fine-tuning** and evaluation workflow, including model/tokenizer export to Google Drive. |
| `arabic/Gemini_Arabic_Campaign_Generation.ipynb` | Gemini API-based **Arabic** post generation, platform profiles, structured response parsing, and hashtag post-processing. |
| `data/dataset_50k_FINAL_CLEANED.zip` | Compressed English fashion-marketing dataset (50,000 records, 25 columns). |

## Dataset

- **Records:** 50,000
- **Columns:** 25
- **Format:** CSV inside ZIP
- **Contents:** Fashion/product information, campaign and audience attributes, and text/hashtag targets for the three post variations.
- **Size:** Approximately 9.7 MiB compressed (CSV approximately 118 MiB uncompressed).

The ZIP is kept compressed because the CSV exceeds GitHub's usual **100 MiB per-file** Git limit. Before publishing the dataset publicly, the team must confirm its **origin, license/redistribution rights, and absence of confidential information**.

## English workflow — T5-Small

1. Upload the dataset ZIP to the Google Colab notebook.
2. Unzip and read the CSV in the notebook environment.
3. Transform 50,000 dataset rows into three task-specific training examples each (**150,000 pairs** before splitting).
4. Fine-tune `t5-small` on the prepared dataset using Hugging Face Transformers.
5. Evaluate generated captions/hashtags and export the trained model, tokenizer, and supporting files to Google Drive.

**Important:** The actual fine-tuned model weights and tokenizer export are **not present** in this package. The notebook contains the *training code*, not a standalone trained-model checkpoint. Publishing weights requires a separate decision about storage and licenses.

**Reproduction note:** The training notebook includes a Google Colab file-upload step and a CSV path tied to the original extracted filename. Confirm the uploaded ZIP/CSV filename and update the notebook's path if needed. Training requires suitable compute and compatible library versions; successful reproduction is not claimed here.

## Arabic workflow — Gemini

The Gemini notebook uses a structured response schema and explicit platform profiles. Its post-processing step cleans and normalizes hashtags and text formatting.

| Platform | Configured hashtag count |
| --- | ---: |
| Instagram | 20 |
| Facebook | 6 |
| TikTok | 5 |
| Websites/Ads | 5 |

### API-key configuration

The shareable notebook has been **sanitized** to read `GEMINI_API_KEY` from **Google Colab Secrets** (or an existing environment variable). Never store API keys directly in notebook cells or GitHub.

1. Create a valid Gemini API key in the provider console.
2. In Google Colab, open **Secrets** and add a secret named `GEMINI_API_KEY` with notebook access enabled; alternatively set the variable in a secure execution environment.
3. Run the notebook. The initialization cell reads the configured secret.

**Security incident:** An earlier source notebook contained a hard-coded live-looking Gemini API key. Its owner must **revoke/rotate that key** independently; editing the notebook does not invalidate an exposed credential. Do not publish the original notebook.

## Shared contributions

| Contributor | GitHub | Work |
| --- | --- | --- |
| Menna Ahmed Amer | [https://github.com/menna-ahmed-amer] | Arabic & English Text and Hashtag Generation (collaborative) |
| Manal Ramadan Ebrahim | [https://github.com/manalramadan111] | Arabic & English Text and Hashtag Generation (collaborative) |

For shared changes, use accurately attributed individual commits or a `Co-authored-by` trailer when the commit genuinely reflects joint work. Do not upload duplicate copies of the same code solely to create separate contributor records.

## Publishing notes

- Upload the **contents** of this module folder into `ai/text_hashtag_generation/` inside the shared repository, not the ZIP itself as the sole source artifact.
- Keep notebook outputs cleared of credentials and personal environment details.
- Ask the team to confirm whether the data ZIP may be published publicly.
- Store large model checkpoints in an appropriate model registry or Git LFS if the team decides to distribute them; do not assume they are in this archive.
- Confirm and document dependency versions when you have tested a reproducible run.
