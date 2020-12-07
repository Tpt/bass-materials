Bass dataset and code
=====================

This repository contains the source code used for the implementation of the *Bass* approach presented in [the under review paper "Neural Knowledge Base Repairs" by Thomas Pellissier Tanon and Fabian Suchanek](https://openreview.net/forum?id=gr5FsBVCkJp).

Bass aims at doing automated knowledge base curation.
It makes use of the advances in neural network research to improve the automated correction of constraint violations.
It is a deep learning refinement of ["Learning  how  to  correct a  knowledge  base  from  the  edit  history"](https://doi.org/10.1145/3308558.3313584), and similarly uses the edits that solved some violations in the past to infer how to solve similar violations in the present.
Bass makes use of the graph content, literal embeddings, and features extracted from Web pages to improve its performance.
An experimental evaluation on Wikidata shows significant improvements over baselines.
The evaluation code is provided in this repository.

Only a sample of the evaluation dataset is provided in this git repository. The full dataset is [available on FigShare](https://doi.org/10.6084/m9.figshare.13338743).

## Bass code

The Bass implementation is provided as a Jupyter Notebook named `corrections_learning.ipynb`. It requires Python 3.6+, Tensorflow 2.0+ and the [`tokenizer` Python library](https://github.com/huggingface/tokenizers) (`pip3 install tokenizers`).
Because only a sample of the dataset is provided in this repository because of git space constraints, performances are slightly different from the paper evaluation.
We also increased the maximal number of epochs to 20 to allow more training on this smaller dataset.

To reproduce the evaluation on the complete dataset please replace the provided sample dataset by the one [shared on FigShare](https://doi.org/10.6084/m9.figshare.13338743).

## Dataset

The dataset is composed of:
1. The file `constraints.tsv` contains the definition of Wikidata constraints. Each constraint is a row of this tab-separated file.
2. The directory `constraint-corrections`. Each file is compressed with gzip. The files' content is tab-separated and is using the following columns:
   1. constraint id
   2. revision that fixed the constraint violation
   3. first violation triple subject
   4. first violation triple predicate
   5. first violation triple object
   6. second violation triple subject (blank if no second violation triple)
   7. second violation triple predicate (blank if no second violation triple)
   8. second violation triple object (blank if no second violation triple)
   9. separator (not useful)
   10. subject of the first triple in the correction
   11. predicate of the first triple in the correction
   12. object of the first triple in the correction
   13. is the first triple in the correction an addition or a deletion (`<http://wikiba.se/history/ontology#deletion>` for a deletion and `<http://wikiba.se/history/ontology#addition>` for an addition)
   14. subject of the second triple in the correction (might not exist)
   15. predicate of the second triple in the correction (might not exist)
   16. object of the second triple in the correction (might not exist)
   17. is the second triple in the correction an addition or a deletion (`<http://wikiba.se/history/ontology#deletion>` for a deletion and `<http://wikiba.se/history/ontology#addition>` for an addition) (might not exist)
   18. Description of the subject of the first violation triple encoded in JSON
   19. Description of the object of the first violation triple encoded in JSON (might be empty for literals)
   20. Description of the term of the second triple that has not already be described by the two previous descriptions. (might be empty for literals or if there is no second triple)

