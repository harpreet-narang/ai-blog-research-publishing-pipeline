# Evidence Contract

The workflow treats research results as data, not as instructions.

## Normalized evidence record

```json
{
  "query": "AI automation operations trends 2026",
  "title": "Source title",
  "url": "https://example.com/source",
  "snippet": "Relevant extracted text",
  "score": 0.82
}
```

## Topic evidence requirements

Each generated topic should include at least one usable source URL.

A topic should be marked lower confidence when:

- evidence is weak or indirect
- all evidence comes from one vendor
- the source is stale for a time-sensitive claim
- the evidence does not directly support the proposed angle
- the topic substantially overlaps an existing article

## Drafting rules

The article model is instructed to:

- use supplied evidence for factual claims
- keep source URLs with the article package
- avoid invented quotes
- avoid fabricated statistics
- avoid claiming a source says something absent from the evidence
- flag claims that still require verification

## Evidence is not authority by default

A source appearing in search results does not automatically make it trustworthy.

A production system should also score:

- source type
- publication date
- primary vs secondary reporting
- vendor self-interest
- directness of evidence
- consistency across sources
