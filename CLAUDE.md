# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a Galaxy tool wrapper for Stanford CoreNLP, enabling NLP annotation pipelines through the Galaxy platform. The tool provides access to various CoreNLP annotators (tokenization, POS tagging, NER, parsing, coreference, sentiment analysis) with multiple output formats.

## Architecture

### Galaxy Tool Definition Structure

The tool is defined in `stanford_corenlp.xml` following Galaxy's tool wrapper XML schema:

- **Versioning**: Version numbers are defined in `macros.xml` using tokens `@VERSION@` (CoreNLP version: 4.5.7) and `@VERSION_SUFFIX@` (wrapper version: 2)
- **Container**: Runs CoreNLP via Docker container `ksuderman/corenlp:@VERSION@`
- **Command Template**: Uses Cheetah template syntax (`#if`, `#else`) to build command-line arguments based on user selections
- **Input Parameters**:
  - `annotators`: Selection of annotation pipeline (tokenize, pos, ner, parse, coref, sentiment)
  - `format`: Output format (json, conll, conllu, text, xml)
- **Output Handling**: CoreNLP writes files with `.out` or `.{format}` extensions; the wrapper copies these to Galaxy's expected output location

### Annotator Dependencies

Annotators have implicit dependencies that the wrapper handles:
- `tokenize` → tokenize only
- `pos` → tokenize, pos, lemma
- `ner` → tokenize, pos, lemma, ner
- `parse` → tokenize, pos, lemma, ner, parse
- `coref` → tokenize, pos, lemma, ner, parse, coref
- `sentiment` → tokenize, pos, lemma, parse, sentiment

## Testing

Galaxy tools use embedded test cases in the XML file (lines 55-112 in `stanford_corenlp.xml`):

### Test Data
- `test-data/input.txt`: Basic text input for tokenization, parsing tests
- `test-data/sa-input.txt`: Sample text for sentiment analysis
- `test-data/2.txt`: Multi-sentence text for tokenization testing
- `test-data/*.conll`, `test-data/*.conllu`: Expected outputs for comparison

### Running Tests
Tests are executed by the Galaxy test framework and output results to `tool_test_output.html` and `tool_test_output.json`.

### Test Assertions
- JSON tests: Use `has_json_property_with_text` to verify specific properties
- File comparison: Use `file="expected.txt"` to compare outputs
- Content assertions: Use `has_text`, `has_n_lines`, `is_valid_xml`

## Output Format Limitations

Not all annotation types can be fully represented in all output formats:
- CoNLL and CoNLL-U formats do not include sentiment analysis annotations
- Dependency parse tree structures are best rendered in JSON
- XML and text formats have limited structured annotation support
