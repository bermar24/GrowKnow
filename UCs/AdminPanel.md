# 1 Use-Case Name

Admin Panel: Review, Edit, and Publish News Drafts

## 1.1 Brief Description

An admin manages news drafts from automation or manual creation. They can browse, open, review, edit, approve, publish, or save as draft. If no drafts exist the system shows options. Published content is indexed. Notification is optional.

---

# 2 Flow of Events

## 2.1 Basic Flow

1. **Admin:** Log in.
2. **System:** Check credentials. If valid show Admin Dashboard.
3. **Admin:** Choose “News drafts.”
4. **System:** Load draft list and history. Decision: *Drafts loaded?*

   * **Yes:** continue to 5.
   * **No:** go to Alt Flow “Empty State.”
5. **Admin:** Open a draft.
6. **System:** Show selected draft.
7. **Admin:** Review and edit.
8. **Decision: Approve?**

   * **No:** go to Alt Flow “Approve = No.”
   * **Yes:** continue.
9. **Decision: Publish?**

   * **No:** go to Alt Flow “Approve = No.”
   * **Yes:** **Admin:** Click “Publish article.”
10. **System:** Publish to website → **OpenSearch:** Index content → **System:** Write audit log → **Email/ESP optional:** Notify.
11. **System:** Return to Dashboard.

### 2.1.1 Alternative Flows

**A. Invalid login**

* **System:** Reject credentials and show error.
* **Admin:** Reattempt login.

**B. Approve = No or Publish = No**

* **Admin:** Select “Save as draft.”
* **System:** Store draft version. Write audit log. Return to dashboard.

**C. Empty State**

* **System:** Show options. Decision: *Which option?*

  1. **Import latest automation output** → **System:** Pull from n8n inbox. Create draft. Open editor.
  2. **Generate now** → **Admin:** Trigger n8n run → **System:** Store run id → On callback create draft. Open editor.
  3. **Create manual draft** → **System:** Insert empty draft. Open editor.
  4. **Duplicate last published** → **System:** Copy last article as draft. Open editor.
  5. **Adjust filters** → **Admin:** Reset filters → **System:** Reload list.

**D. Notification off**

* **Admin/System:** Skip email step. Indexing and audit remain.

**E. System failures**

* **DB save or publish error:** Show error. Draft unchanged.
* **Automation unavailable:** Show fallback. Offer manual draft or duplicate.

## 2.1.2 Postconditions

* **Publish:** Article live. Index updated. Audit written. Notification sent if enabled.
* **Save as draft:** New version stored and visible in list.

## 2.1.3 Termination

* **Admin:** Optional log out.

## 2.1.4 Activity Diagram

Swimlanes: **Admin**, **System**, **OpenSearch**, **Email/ESP**.

### 2.1.4 Activity Diagram

<img width="3454" height="3956" alt="UseCaseAdminLoggedIn" src="https://github.com/user-attachments/assets/686979f2-cc11-408a-8278-453eae655ad7" />

### 2.1.5 Mock-up

<img width="3226" height="3622" alt="Group 2" src="https://github.com/user-attachments/assets/462c742c-c9f8-49c4-88d1-b3d33002a5a8" />



### 2.1.6 Narrative
```gherkin
Feature: Admin Panel - Review, Edit, and Publish News Drafts
  As an admin
  I want to manage news drafts
  So that I can review, edit, publish, or save them

  Background:
    Given the admin is logged in
    And the system has validated credentials

  # --- Basic Flow ---
  Scenario: Admin reviews and publishes a draft
    When the admin opens the "News drafts" section
    And drafts are available
    And the admin opens a draft
    And the admin reviews and approves the draft
    And the admin chooses to publish it
    Then the system publishes the article
    And the system indexes the content in OpenSearch
    And the system writes an audit log
    And the system sends a notification email (if enabled)
    And the admin returns to the dashboard

  # --- Alternative Flows ---
  Scenario: Invalid login
    Given the admin enters invalid credentials
    Then the system rejects the login and displays an error message
    When the admin retries with valid credentials
    Then the system grants access

  Scenario: Admin saves as draft instead of publishing
    When the admin opens a draft
    And the admin reviews but does not approve or publish
    Then the admin saves it as draft
    And the system stores the draft version and writes an audit log

  Scenario: Empty State - no drafts exist
    Given there are no existing drafts
    When the admin opens the "News drafts" section
    Then the system displays creation options:
      | Option                     |
      | Import latest automation output |
      | Generate now               |
      | Create manual draft        |
      | Duplicate last published   |
      | Adjust filters             |

  Scenario: Notification disabled
    Given notifications are turned off
    When the admin publishes an article
    Then the system indexes and logs the action but skips sending emails

  Scenario: System failure during publishing
    When a database save or publish error occurs
    Then the system shows an error message
    And the draft remains unchanged
```
This Narrative is implemented in a [seperate document](https://github.com/bermar24/GrowNow/blob/main/src/test/resources/features/AdminPanel.feature).

## 2.2 Alternative Flows
### Invalid Login
- The system rejects invalid credentials and displays an error message.
- The admin can attempt to log in again.

### Approve = No / Publish = No
- The admin chooses “Save as draft.”
- The system stores the draft version, logs the action, and returns to the dashboard.

### Empty State
When no drafts exist, the system displays available options:
- Import latest automation output: pulls drafts from n8n inbox.
- Generate now: triggers n8n run, creates draft on callback.
- Create manual draft: inserts empty draft.
- Duplicate last published: copies last article as a new draft.

### Notification Off
- The system skips sending email/ESP notifications, but indexing and audit logging still occur.

# 3 Special Requirements
- The system must index published content in OpenSearch.
- Audit logs must be written for every draft edit, save, or publish action.
- The system must support optional notifications via email/ESP.
- Draft editing must allow inline content changes with validation.
- The system must handle automated drafts via n8n workflow integration.

# 4 Preconditions
## 4.1 Login
- Admin must have valid credentials.

# 5 Postconditions
- If published: content is live on the website, indexed in OpenSearch, audit logs written, notifications sent if enabled.
- If saved as draft: new draft version is stored and visible in the draft list.

# 6 Extension Points
- Integration with n8n workflows for automated content ingestion.
- Optional notification system integration via email/ESP.
- OpenSearch indexing for searchability of published articles.
- Audit logging for compliance and tracking changes.