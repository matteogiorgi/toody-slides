<style>
  body {
      max-width: 90rem;
  }
  h2 {
      text-align: center;
      text-decoration: underline;
      color: #888888;
  }
</style>


<div style="margin-top: 80px;">
# `Matcher` vs `PhraseMatcher`

<div style="display: flex; justify-content: space-between;">
<div style="flex: 1; border-radius: 4px; background: #e9edf3; padding: 1.5rem; margin-right: 5px; margin-left: 5px;">
## `Matcher`

<div style="font-size: 70%;">
```python
import spacy
from spacy.matcher import Matcher

nlp = spacy.load("it_core_news_sm")
matcher = Matcher(nlp.vocab)

pattern = [{"POS": "NOUN"}, {"POS": "ADJ"}]
matcher.add("NOUN_ADJ_PATTERN", [pattern])


doc = nlp(
    "Il mercato azionario ha mostrato"
    "una crescita costante."
)

matches = matcher(doc)
# mercato azionario
# crescita costante
```
</div>
</div>

<div style="flex: 1; border-radius: 4px; background: #e9edf3; padding: 1.5rem; margin-right: 5px; margin-left: 5px;">
## `PhraseMatcher`

<div style="font-size: 70%;">
```python
import spacy
from spacy.matcher import PhraseMatcher

nlp = spacy.load("it_core_news_sm")
phrase_matcher = PhraseMatcher(nlp.vocab)

phrases = ["intelligenza artificiale", "realtà virtuale"]
patterns = [nlp(text) for text in phrases]
phrase_matcher.add("TECH_PATTERNS", patterns)

doc = nlp(
    "L’intelligenza artificiale e la realtà virtuale "
    "sono due delle tecnologie più innovative."
)

matches = phrase_matcher(doc)
# intelligenza artificiale
# realtà virtuale
```
</div>
</div>
</div>
</div>
