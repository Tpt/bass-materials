Bass dataset and code
=====================

This repository contains a sample of Bass dataset and code.

The full dataset is [available on FigShare](https://doi.org/10.6084/m9.figshare.13338743)

## Bass code

The Bass implementation is provided as a Jupyter Notebook. It requires Python 3.6+, Tensorflow 2.0+ and the [`tokenizer` Python library](https://github.com/huggingface/tokenizers) (`pip3 install tokenizers`).
Because only a sample of the dataset is provided in this repository because of git space constraints, performances are slightly different from the paper evaluation.
We also increased the maximal number of epochs to 20 to allow more training on this smaller dataset.

To reproduce the evaluation on the complete dataset please replace the provided sample dataset by the one [shared on FigShare](https://doi.org/10.6084/m9.figshare.13338743).

## Dataset

The dataset is composed of:
1. The file `constraints.tsv` that contains the definition of Wikidata constraints. Each constraint is a row of this tab separated file.
2. The directory `constraint-corrections`. Each file is compressed with gzip. The files content is tab separated and is using the following columns:
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
   15. predicate of the econd triple in the correction (might not exist)
   16. object of the econd triple in the correction (might not exist)
   17. is the second triple in the correction an addition or a deletion (`<http://wikiba.se/history/ontology#deletion>` for a deletion and `<http://wikiba.se/history/ontology#addition>` for an addition) (might not exist)
   18. Description of the subject of the first violation triple encoded in JSON
   19. Description of the object of the first violation triple encoded in JSON (might be empty for literals)
   20. Description of the term of the second triple that has not already be described by the two previous description. (might be empty for literals or if there is no second triple)

