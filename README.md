# Galaxy wrapper for Stanford CoreNLP

This wrapper provides easy access to Stanford CoreNLP pipelines. Users can 
select annotators and the output format.

## Annotators

| Type | Annotators |
|---|---|
| Segmentation | tokenize, spplit |
| Part of speech | tokenize, spplit, pos, lemma |
| Named entity recognition | tokenize, spplit, pos, lemma , ner|
| Dependency parse | tokenize, spplit, pos, lemma, ner, parse |
| Coreference | tokenize, spplit, pos, lemma, ner, parse, coref |
| Sentiment analysis | tokenize, spplit, pos, lemma, parse, sentiment |


## LICENSE

This repository contains an unmodified copy of the 
[Stanford CoreNLP](https://stanfordnlp.github.io/CoreNLP/) package.  Stanford 
CoreNLP is released under the 
[GPL v3 license](https://raw.githubusercontent.com/stanfordnlp/CoreNLP/main/LICENSE.txt).

This will be removed when/if the Stanford CoreNLP package appears on `conda-forge`
or other location supported by Galaxy's dependency resolvers.