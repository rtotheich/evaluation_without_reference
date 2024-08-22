# Extrinsic Evaluation of MT without Reference Translations
<h2>Project Description</h2>
<p>Standard metrics such as BLEU depend on expensive reference translations.
We propose an unsupervised alternative that
compares performance on downstream tasks with and without back-translation.
Back-translation usually degrades performance, but the amount of degradation depends on
the task and the quality of the translations.
We will select tasks that differentiate systems,
and use the degradation on these tasks to compare systems.
Much of the literature these days prefers extrinsic evaluations on downstream
tasks over intrinsic metrics.  In this spirit, we view translation as a small step in a larger pipeline.
Ideally, we would like to replace intrinsic metrics such as BLEU with end-to-end evaluations of the pipeline.
We view the proposed back-translation evaluation as an approximation of this end-to-end evaluation.</p>
<p>With the fine tuned monolingual model as a baseline, we back-translate (from and back to English) the validation set into a total of 11 languages using three MT models: <a href="https://huggingface.co/facebook/mbart-large-50-many-to-many-mmt">mBART-large-50</a>, <a href="https://huggingface.co/Helsinki-NLP">Opus-MT</a>, and <a href="https://huggingface.co/docs/transformers/en/model_doc/t5">T5</a>. The translation languages are German (de), Italian (it), Spanish (es), Estonian (et), French (fr), Russian (ru), Finnish (fi), Vietnamese (vi), Hindi (hi), Chinese (zh), and Arabic (ar).</p>
<h2>Methodology</h2>
<p>We start with a monolingual pre-trained language model (PLM) and fine-tune it on the following task-specific datasets: <a href="https://huggingface.co/datasets/nyu-mll/glue/viewer/rte">GLUE-RTE</a>, <a href="https://paperswithcode.com/dataset/food-recall-incidents-dataset">Food Recall Incidents (Product and Hazard, coarse)</a>, <a href="https://huggingface.co/datasets/dair-ai/emotion">Emotion</a>, <a href="https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge/data">Toxicity</a>, <a href="https://semeval.github.io/SemEval2024/">Semeval2024</a>, and <a href="https://research.google/blog/announcing-the-patent-phrase-similarity-dataset/">Google Patent Similarity</a>.</p>
<h2>Model Hyperparameters</h2>
<p>
  <ul>
    <li>For the RTE task, we use the <a href="https://huggingface.co/FacebookAI/roberta-base">RoBERTa-base</a> model. We train for 10 epochs with a max sequence length of 512, a batch size of 8, a learning rate of 1e-5, a seed of 42.</li>
    <li>For the Emotion task, we use the <a href="https://huggingface.co/distilbert/distilbert-base-uncased">Distilbert-base-uncased</a> model. We train for 2 epochs with a learning rate of 2e-5, a batch size of 64, and a weight decay of 0.01.</li>
    <li>For both the Food Recall Hazard and Product task, we instantiate the <a href="https://huggingface.co/FacebookAI/roberta-base">RoBERTa-base</a> model using the Hugging Face Trainer API. We train for 10 epochs with a batch size of 16, a learning rate of 5e-5, and a weight decay of 0.01.</li>
    <li>For the Semeval 2024 task, we train the <a href="https://huggingface.co/distilbert/distilbert-base-uncased">Distilbert-base-uncased</a> model for 3 epochs with a batch size of 32, a learning rate of 2e-5, and a weight decay of 0.01.</li>
    <li>For the toxicity task, we train the <a href="https://huggingface.co/distilbert/distilbert-base-uncased">Distilbert-base-uncased</a> model for 2 epochs with a batch size of 16, a learning rate of 2e-5, and a weight decay of 0.01.</li>
    <li>For the Google Patent Similarity task, we train on the <a href="https://huggingface.co/anferico/bert-for-patents">BERT-for-patents</a> model for 3 epochs with a batch size of 8 and a learning rate of 2e-5.</li>
  </ul>
</p>
