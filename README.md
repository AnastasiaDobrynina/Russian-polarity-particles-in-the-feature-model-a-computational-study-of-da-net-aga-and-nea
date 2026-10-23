# Russian polarity particles in the feature model: a computational study of *da*, *net*, *aga* and *nea*

Final project for the course *Linguistic Data: Quantitative Analysis and Visualisation* (HSE, 2026).
Author: Anastasia Dobrynina

The project tests which features of the feature model (Roelofsen & Farkas 2015; Farkas & Roelofsen 2019) Russian response particles realize. It uses corpus data from the Russian National Corpus, automatic annotation with an LLM (Qwen2.5-3B-Instruct), distributional analysis, and ruBERT embeddings with PCA and k-means clustering.

## Repository structure

### Notebook
| File | Description |
|---|---|
| `Dobrynina_Linguistic_data_project.ipynb` | The whole pipeline: data collection, LLM annotation, validation, distributional analysis, embeddings |

### Input data (needed to run the notebook)
| File | Description |
|---|---|
| `Spoken.csv` | RNC Spoken Corpus: particle directly after a dash |
| `Spoken with left.csv` | RNC Spoken Corpus: particle after a short lead-in following a dash |
| `murco.csv` | RNC Multimedia Corpus (MURCO): particle with a capital letter |

All three are RNC exports separated by `;`.

### LLM annotation (Step 2)
| File | Description |
|---|---|
| `prompt.txt` | System prompt and few-shot examples used for the annotation |
| `dataset_input_snapshot.csv` | Filtered dataset sent to the model (1,678 rows, with `row_id`) |
| `llm_raw_outputs2.jsonl` | Raw model outputs, one JSON line per row (checkpoint) |
| `dataset_annotated2.csv` | Final annotated dataset, the input for Steps 3–4 |

### Validation
| File | Description |
|---|---|
| `validation_sample2.xlsx` | Validation sample with manual (gold) annotation |
| `validation_results2.csv` | Agreement and Cohen's kappa for each field |

### Results
| File | Description |
|---|---|
| `step4_counts.csv` | Counts: particle × response type × question type |
| `step4_proportions.csv` | The same table as row proportions |
| `step5_embeddings.npy` | ruBERT embeddings of the particle tokens |
| `figures/heatmap_response_types.png` | Heatmap of response types by particle and question type |
| `figures/stacked_bars.png` | Stacked bar charts of agree/reverse responses |
| `figures/step5_pca.png` | PCA of the ruBERT embeddings |
| `figures/step5_kmeans.png` | k-means clusters on the PCA plane |

## How to run

1. Put the notebook and all files listed above into one folder (e.g. on Google Drive).
2. In the notebook, set `WORK_DIR` to the path of that folder.
3. Run the cells in order. The LLM annotation (Step 2) does **not** need to be re-run: its cells are commented out, and Step 3 loads `dataset_annotated2.csv`. Re-running the annotation requires a GPU runtime.
4. Steps 3–4 run on CPU.

## Requirements

Google Colab or Python 3.10+ with:
`pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `statsmodels`, `scikit-learn`, `torch`, `transformers`, `openpyxl`, and (only for re-running the annotation) `bitsandbytes`, `accelerate`.

## Models

- Annotation: [Qwen/Qwen2.5-3B-Instruct](https://huggingface.co/Qwen/Qwen2.5-3B-Instruct)
- Embeddings: [DeepPavlov/rubert-base-cased](https://huggingface.co/DeepPavlov/rubert-base-cased)

## References

- Esipova, M. (2021). Polar responses in Russian across modalities and across interfaces. *Journal of Slavic Linguistics*, 29(3), 1–11.
- Farkas, D. F., & Roelofsen, F. (2019). Polarity particles revisited. *Semantics & Pragmatics*, 12(15), 1–25.
- Roelofsen, F., & Farkas, D. F. (2015). Polarity particle responses as a window onto the interpretation of questions and assertions. *Language*, 91(2), 359–414.
