# Dataset Audit Summary

The source archive was audited before model training. It contained 188 readable JPEGs: 89 supplied Normal, 75 supplied Celiac, and 24 supplied Doubtful.

The primary analysis excluded the supplied-Doubtful images. Five byte-identical supplied-Normal copies were removed, yielding a canonical analysis set of 159 images: 84 supplied Normal and 75 supplied Celiac.

Six visually related primary pairs were retained as fixed groups for the held-out split. Four exact-copy components containing nine original files were reduced to five keepers. Fifty-eight candidate near-pairs were manually reviewed and did not create additional groups. A cross-set relation between `Celiac/c2.jpg` and `Doubtful/d11.jpg` was retained as an audit note, with the Doubtful image held outside the primary analysis.

The full audit report is intentionally excluded from the lightweight GitHub upload because its file size exceeds the web uploader limit. The canonical manifest, frozen protocol, and reproducible audit code remain in this repository.
