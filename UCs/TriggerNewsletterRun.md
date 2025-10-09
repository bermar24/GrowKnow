# 1 Use-Case Name

Trigger Newsletter Run (Automation → Review → Publish)

## 1.1 Brief Description

n8n runs on a fixed schedule and generates a news article draft from vetted sources. The system stores and indexes the draft, queues it for review, and notifies the admin. The admin reviews, optionally edits, and approves. The system publishes and records run metrics.

---

# 2 Flow of Events

## 2.1 Basic Flow

1. **Automation (n8n):** schedule fires (every 12–24h).
2. **Automation:** fetch sources / search news.
3. **Automation:** deduplicate.
4. **Automation:** extract key points.
5. **Automation:** classify and tag.
6. **Automation:** generate news article draft.
7. **Automation → System:** send draft to system.
8. **System:** store draft in DB.
9. **System:** index for search.
10. **System:** queue for review.
11. **System → Admin:** notify admin (email/link).
12. **Admin:** open review link.
13. **Admin:** review draft.
14. **Decision – Approve?**

    * **Yes:** **Admin:** click **Publish**.
15. **System:** publish to website.
16. **System:** log run and metrics.
17. **End.**

## 2.1.2 Alternative Flows

* **Approve = No**

  * **Admin:** edit draft.
  * Return to step 14 and decide again.

* **Notification not received**

  * **System:** link still available in review queue; admin opens from dashboard instead.

* **Minor edits before publish**

  * **Admin:** edits draft after opening link.
  * Continue with **Approve = Yes** then publish.

* **Indexing skipped for privacy** (rare)

  * **System:** can omit search indexing for drafts flagged confidential; review still proceeds.

* **Publish blocked** (validation fails, missing fields)

  * **System:** reject publish, show errors to admin.
  * **Admin:** fixes content, retry from step 14.

## 2.1.3 Postconditions

* Article is live on the website.
* Search index updated for the article.
* Run metrics recorded (timestamps, items processed, dedupe count, review latency, publish status).

## 2.1.4 Special Requirements

* Scheduled cadence configurable (12–24h).
* Review link must be single-click to editor with draft loaded.
* Metrics must be queryable for reporting.

## 2.1.5 Termination

* Use case ends after **Log run & metrics** or after admin defers approval (draft remains queued).


### 2.1.6 Activity Diagram

<img width="2378" height="2793" alt="AutomationUseCase" src="https://github.com/user-attachments/assets/7de975e0-5eb6-4ac0-9389-d8c36e659ce1" />

### 2.1.7 Mock-up
(n/a)

### 2.1.8 Narrative
```gherkin
```

## 2.2 Alternative Flows
(n/a)

# 3 Special Requirements
(n/a)

# 4 Preconditions
## 4.1 Login
The user has to be logged in to the system.

# 5 Postconditions
(n/a)

# 6 Extension Points
(n/a)
