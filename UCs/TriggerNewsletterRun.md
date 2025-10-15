# 1 Use-Case Name

Trigger Newsletter Run (Automation → Review → Publish)

## 1.1 Brief Description

n8n runs on a fixed schedule and generates a news article draft from vetted sources. The system stores and indexes the draft, queues it for review, and notifies the admin. The admin reviews, may edit, approves, and publishes. The system records run metrics.

---

# 2 Flow of Events

## 2.1 Basic Flow

### 2.1.0 Automation (n8n)

1. **Schedule fires** every 12–24h.
2. **Fetch sources** and search news.
3. **Deduplicate** items.
4. **Extract key points.**
5. **Classify and tag.**
6. **Generate news article draft.**
7. **Send draft to System.**

### 2.1.1 System intake

8. **Store draft in DB.**
9. **Index for search.**
10. **Queue for review.**
11. **Notify Admin** via email or link.

### 2.1.3 Admin review and publish

12. **Admin opens review link.**
13. **Admin reviews draft.**
14. **Decision: Approve?**

    * **Yes:** go to 15.
    * **No:** see Alternative Flows A or C.
15. **Admin clicks Publish.**
16. **System publishes to website.**
17. **System logs run and metrics.**
18. **End.**

---

## 2.1.2 Alternative Flows

**A. Approve = No**

* **Admin edits draft.**
* Return to step 14.

**B. Notification not received**

* **System** keeps link in review queue.
* **Admin** opens draft from dashboard.
* Continue at step 13.

**C. Minor edits before publish**

* **Admin** edits after opening link.
* Continue with Approve = Yes at step 15.

**D. Indexing skipped for privacy**

* **System** omits search indexing for confidential drafts.
* Review proceeds. Publishing unaffected.

**E. Publish blocked by validation**

* **System** rejects publish and shows errors.
* **Admin** fixes content.
* Retry from step 14.

---

## 2.1.3 Postconditions

* Article live on website.
* Search index updated, unless confidential.
* Run metrics recorded: timestamps, items processed, dedupe count, review latency, publish status.

## 2.1.4 Special Requirements

* Schedule configurable between 12 and 24 hours.
* Review link opens editor with draft loaded in one click.
* Metrics queryable for reporting.

## 2.1.5 Termination

* After logging run and metrics.
* Or after admin defers approval, draft remains queued.

### 2.1.6 Activity Diagram

<img width="1654" height="2895" alt="UsecaseAutomation" src="https://github.com/user-attachments/assets/09b6e5dc-12f5-4337-adf8-08a3075d60d1" />

<img width="1654" height="2904" alt="UseCaseAdminWithLink" src="https://github.com/user-attachments/assets/020106d0-2c27-4226-8575-8d3570abd732" />



### 2.1.7 Mock-up

<img width="3188" height="1887" alt="Group 1" src="https://github.com/user-attachments/assets/7b0392f7-ac8f-4203-a088-b5c6285fa5ab" />


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
