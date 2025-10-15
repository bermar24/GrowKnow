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
