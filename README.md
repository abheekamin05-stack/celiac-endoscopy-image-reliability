# Reliability-Aware Review Prioritization for Celiac Endoscopy Images

This student-led, exploratory project evaluates whether simple image-reliability signals can help prioritize review of a particularly consequential classifier error: an endoscopy image supplied with a Celiac label that a model predicts as Normal.

It is **not** a diagnostic system, clinical validation study, or patient-level analysis. The public image archive has no patient identifiers, pathology confirmation, device metadata, or clinical outcomes.

## Question

After a model predicts an image is Normal, can a fixed score combining weak Normal confidence, prediction instability, and technical-image-quality proxies identify more supplied-Celiac false-normal images for review than confidence alone?

## Dataset and safeguards

The source archive contained 188 readable JPEGs. The primary analysis excluded 24 supplied-Doubtful images and removed five byte-identical Normal duplicates, producing a canonical set of **159 images**: 84 supplied Normal and 75 supplied Celiac.

Related-image groups were kept together in five fixed, stratified held-out folds. The audit manifest and frozen protocol are included in `docs/`; the larger full audit report is available separately from the project author.

## Model and main result

An ImageNet-pretrained ResNet-18 was trained in five group-disjoint folds, producing one held-out prediction for each of the 159 images.

| Held-out classifier result | Count |
| --- | ---: |
| Correct Normal predictions | 74 / 84 |
| Correct Celiac predictions | 59 / 75 |
| Accuracy | 133 / 159 (83.6%) |
| Celiac sensitivity | 59 / 75 (78.7%) |
| Normal specificity | 74 / 84 (88.1%) |

Among 90 images predicted Normal, 16 had a supplied Celiac label. At review rates of 10%, 20%, and 30%, confidence-only prioritization identified **4, 6, and 9** of those 16 images; the equal-weight combined score identified **4, 4, and 7**. At the prespecified 20% review rate, the combined score was therefore 2 cases worse than confidence alone. A group-resampled bootstrap (2,000 replicates) gave a 95% interval of **[-6, +1]** for this paired difference.

The result does not support claiming that the combined score improves review prioritization on this dataset. Crop and layout sensitivity analyses are retained in the notebook and reported in the project materials.

## Repository layout

```text
notebooks/phase5_pipeline.ipynb       Reproducible Phase 5 workflow
docs/                                 Audit, protocol, and literature materials
results/                              Small derived result summaries only
```

## Reproducing the workflow

1. Download the source archive from its original provider. Do not add the image archive to this repository.
2. Open `notebooks/phase5_pipeline.ipynb` in Google Colab with a GPU runtime.
3. Upload the source archive when prompted by the notebook.
4. Run the notebook in order. It rebuilds the audit, fixed folds, held-out ResNet-18 predictions, reliability features, rankings, bootstrap analysis, crop sensitivity analysis, and reports.

The notebook intentionally uses `/content/celiac_reliability_phase5` as a temporary Colab output directory. Generated images, checkpoints, and large intermediate files are excluded from version control.

## Limitations

- Supplied image labels are not pathology-confirmed patient-level ground truth.
- The sample is small and may contain acquisition/layout differences unrelated to disease.
- No result here establishes clinical safety, diagnostic accuracy in practice, or a recommendation for medical use.
- The technical-quality proxies are exploratory and only partly validated.

## Citation

If you reference this project, please cite the repository and link to the original dataset source listed in the notebook. A manuscript/preprint citation can be added here once public.

## License

The original code in this repository is available under the MIT License. The source images and any third-party materials remain subject to their original terms.
