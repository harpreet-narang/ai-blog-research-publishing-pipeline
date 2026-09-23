# Architecture

## Goal

Build a content pipeline where research and editorial decisions happen **before** publishing.

The pipeline is intentionally split into stages so each stage can be inspected, replaced, tested, or retried independently.

## Stages

### 1. Intake
Receives business context, audience, content goal, and existing topics.

### 2. Research query planner
Uses the LLM to create focused search queries. The planner is not allowed to write the article.

### 3. Discovery research
Runs the queries through a web-research adapter and normalizes the returned sources.

### 4. Topic opportunity generator
Creates five evidence-backed topics. Each opportunity must reference source URLs from the evidence pack.

### 5. Human topic gate
The workflow pauses until a reviewer selects one topic.

### 6. Deep research
Runs a second research pass around the chosen angle.

### 7. Article generator
Produces structured article content and metadata from the selected topic and deep-research evidence.

### 8. Hero-image brief
Generates visual direction separately from the article.

### 9. Editorial gate
A reviewer approves, rejects, or requests a revision.

### 10. Revision
Reviewer feedback is applied to the article package. The revised version requires a second approval.

### 11. CMS payload
The workflow converts the approved article into a normalized publishing payload.

### 12. Optional publisher
A disabled HTTP adapter shows where a real CMS integration belongs.

## Separation of responsibilities

```text
research provider → evidence
LLM → interpretation and drafting
human → topic and publishing decisions
CMS adapter → external side effect
```

No single component is trusted to perform all four roles.

## Why two research passes?

The first pass answers:

> What topics appear worth investigating?

The second pass answers:

> What evidence supports this specific article?

This reduces the chance that a broad discovery snippet becomes the sole foundation for a detailed claim.

## Production extensions

A production implementation may add:

- persistent topic database
- content calendar
- scheduled research
- email/Slack/Telegram approval
- image-generation API
- CMS-specific schema mapping
- article version history
- plagiarism/similarity checks
- source freshness thresholds
- analytics feedback after publishing
