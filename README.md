# Extrinsic Evaluation of MT without Reference Translations
Standard metrics such as BLEU depend on expensive reference translations.
We propose an unsupervised alternative that
compares performance on downstream tasks with and without back-translation.
Back-translation usually degrades performance, but the amount of degradation depends on
the task and the quality of the translations.
We will select tasks that differentiate systems,
and use the degradation on these tasks to compare systems.
Much of the literature these days prefers extrinsic evaluations on downstream
tasks over intrinsic metrics.  In this spirit, we view translation as a small step in a larger pipeline.
Ideally, we would like to replace intrinsic metrics such as BLEU with end-to-end evaluations of the pipeline.
We view the proposed back-translation evaluation as an approximation of this end-to-end evaluation.
