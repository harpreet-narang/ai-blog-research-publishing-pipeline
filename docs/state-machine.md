# Pipeline State Machine

The workflow can be thought of as a simple state machine.

```text
RECEIVED
  ↓
RESEARCHING
  ↓
TOPICS_READY
  ↓
WAITING_FOR_TOPIC_SELECTION
  ↓
DEEP_RESEARCH
  ↓
DRAFT_READY
  ↓
WAITING_FOR_EDITORIAL_REVIEW
   ↙       ↓        ↘
REJECTED  REVISION  APPROVED
             ↓
         REVISED_DRAFT
             ↓
      WAITING_FOR_SECOND_REVIEW
          ↙           ↘
      REJECTED       APPROVED
                         ↓
                  READY_TO_PUBLISH
                         ↓
                     COMPLETE
```

## Why explicit state matters

Long-running content automation can span minutes, hours, or days.

Explicit states make it easier to:

- resume after human review
- see where a draft is stuck
- avoid publishing an unapproved version
- distinguish research failure from editorial rejection
- build dashboards later

## Portfolio workflow

The public workflow carries state inside the n8n execution.

A production version would normally persist state to a database so approval links, retries, versions, and publishing history survive independently of one workflow execution.
