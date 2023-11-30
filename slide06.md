<style>
  body {
      max-width: 90rem;
  }
  h2 {
      text-align: center;
      text-decoration: underline;
      color: #888888;
  }
  .sticky-image-container {
      position: -webkit-sticky;
      position: sticky;
      top: 100px;
      align-self: flex-start;
  }
</style>


<div style="margin-top: 80px;">
# TooDY analyser

<div style="display: flex; justify-content: space-between;">
<div style="flex: 1; border-radius: 4px; background: #e9edf3; padding: 1.5rem; margin-right: 5px; margin-left: 5px;">
<div style="font-size: 70%;">
```python
def lexical_analyser(
    doc_requisiti, content1,
    content2, lexical_memory
):
    lexical_patterns = [
        nlp.make_doc(text.strip())
        for text in content2.splitlines()
        if not text.strip().startswith("#")
        and text.strip() != ""
    ]

    matcher = PhraseMatcher(nlp.vocab, attr="LOWER")
    matcher.add("LEXICAL_PATTERNS", lexical_patterns)
    matches = matcher(doc_requisiti)

    results = {}
    for match_id, start, end in matches:
        span = doc_requisiti[start:end]
        line_number = content1.count(
            "\n", 0, span.start_char
        ) + 1

        sentence_start = span.sent.start_char
        highlighted = highlight_specific_instance(
            span.sent.text,
            span.text,
            span.start_char - sentence_start,
            span.end_char - sentence_start,
        )

        highlighted = highlighted.replace(
            "\r", ""
        )

        tag = "neutral"
        if span.text in lexical_memory:
            for label, sentences
            in lexical_memory[span.text].items():
                if highlighted in sentences:
                    tag = label
                    break

        if span.text not in results:
            results[span.text] = []

        results[span.text].append({
            "line": line_number,
            "sentence": highlighted,
            "tag": tag
        })

    results = dict(sorted(results.items()))
    return results
```
</div>
</div>

<div class="sticky-image-container" style="flex: 1; padding: 0rem;">
<img src="../lexical_parser.svg" alt="Descrizione immagine" style="display: block; margin-left: auto; margin-right: auto; width: 800px; height: auto;">
</div>
</div>
</div>
