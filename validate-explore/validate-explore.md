# Lab 6: Validate and Explore AJD Benefits

## Introduction

In this lab, you will use vibe coding to complete the final stage of the journey: repoint the To-Do app to the migrated target collection, validate behavior and data integrity, and explore AJD capabilities for security, scaling, monitoring, and AI in Oracle AI Database 26ai.

Just like Labs 3, 4, and 5, you will guide the AI assistant through structured sprints.

We will follow this 4-step workflow:
1. **Planning**: Crafting the prompt.
2. **Reviewing the plan**: Checking the AI's proposed implementation.
3. **Acting on the plan**: Allowing Cline to execute actions after plan approval.
4. **Validating and adjusting**: Confirming outcomes and correcting if needed.

> **Estimated Time:** 15 minutes

**Note:** AI-generated output is non-deterministic. The instructions below first provide prompts for you to run in Cline and review the results. If you are not happy with the generated output, use the manual `[Optional]` steps in each task to complete the lab with the tested workflow.

---

## Objectives

In this lab, you will:
- Use structured AI-assisted sprints to validate a migrated AJD-backed app
- Repoint the app from source to target collection
- Validate CRUD behavior and migrated data integrity
- Explore AJD benefits: security, scaling, monitoring, and AI integration in 26ai

---

## Prerequisites

This lab assumes you have:
- Completed Lab 5
- The To-Do app from Lab 3
- Migrated data in `todos_target`

---

## Task 1: Sprint 0 — Grounding the AI Session

**Goal:** Establish clear context so the AI assistant understands the app state, migration status, and final validation goals.

### 1. Planning: Crafting the prompt

*How to construct this prompt:* Ground the AI in your current workshop state and define the sprint sequence for this lab.

```text
<copy>
Hi Cline, we are starting Lab 6 in the AJD Mongo workshop.

Context:
- We already built the To-Do app in Lab 3.
- We analyzed source data in Lab 4.
- We migrated data to `todos_target` in Lab 5.
- We now need to validate the migrated app against the target AJD environment.

For this lab, please use a sprint-based approach:
- Sprint 1: Repoint app config from source to target.
- Sprint 2: Validate app CRUD behavior and data integrity.
- Sprint 3: Explore AJD benefits (security, scaling, monitoring, AI in 26ai).

Please acknowledge the plan and confirm readiness for Sprint 1.
</copy>
```

### 2. Reviewing the plan: Checking the AI's proposed implementation

Confirm the AI response includes:
- Clear awareness of current lab status
- A practical sequence for repoint, validate, and explore
- Explicit readiness to begin Sprint 1

*add image: Cline response confirming Sprint 0 grounding and readiness.*

### 3. Acting on the plan: Aligning the session

Acknowledge the AI plan and proceed to Sprint 1.

### 4. Validating and adjusting: Readiness check

Ensure the AI is scoped to this lab only and does not propose unnecessary refactoring or unrelated tooling.

---

## Task 2: Sprint 1 — Repoint the Application to Target Collection

**Goal:** Switch the running app from source to target AJD collection with minimal changes.

### 1. Planning: Crafting the prompt

*How to construct this prompt:* Ask for the exact environment variables and commands required to repoint safely.

```text
<copy>
Let's start Sprint 1.

Please first provide a short implementation plan only (do not execute yet). After I approve, execute the actions.

For execution, tell me exactly which environment variables to update so the To-Do app points to the migrated target AJD collection instead of source. Include the exact export commands and any server restart command needed.
</copy>
```

### 2. Reviewing the plan: Checking the AI's proposed implementation

Verify the AI calls out:
- `SOURCE_MONGO_API_URL` should point to the target URI for this validation run
- `COLLECTION_NAME='todos_target'` (or equivalent collection routing)
- Restart command (`node server.js`)

*add image: Cline response with repointing commands.*

### 3. Acting on the plan: Allowing Cline to execute

Toggle to **Act Mode** and let Cline run the approved Sprint 1 commands:
- `cd path/to/todo-app`
- `export SOURCE_MONGO_API_URL="$TARGET_MONGO_API_URL"`
- `export COLLECTION_NAME='todos_target'`
- `node server.js`

[Optional] If your app uses a different variable name than `SOURCE_MONGO_API_URL`, apply the equivalent target URI variable your app expects.

### 4. Validating and adjusting: Testing the output

Confirm the server starts successfully and no connection errors appear.

*add image: Terminal showing updated env vars and running app.*

---

## Task 3: Sprint 2 — Validate Functionality and Data Integrity

**Goal:** Confirm the repointed app works end-to-end and migrated data is intact.

### 1. Planning: Crafting the prompt

*How to construct this prompt:* Ask the AI for a concise checklist covering UI validation plus SQL-side verification.

```text
<copy>
Great, Sprint 2.

Please first provide a short execution plan only (do not run actions yet). After I approve, execute the validation steps.

Then provide and run a short validation checklist to confirm that after repointing:
1) migrated tasks load correctly in the UI, 
2) CRUD operations still work, and 
3) `todos_target` data integrity is verified in SQL Web.
</copy>
```

### 2. Reviewing the plan: Checking the AI's proposed implementation

Ensure the checklist covers:
- Open app at `http://localhost:3000`
- Add, complete, and delete tasks
- Query target collection in SQL Web
- Compare target rows/documents against source expectations

*add image: Cline validation checklist response.*

### 3. Acting on the plan: Allowing Cline to execute validation

Toggle to **Act Mode** and let Cline execute the approved Sprint 2 validation flow.

1. Open `http://localhost:3000` and verify migrated tasks appear.

![Migrated Tasks](./images/migrated-tasks.png)

2. Test CRUD operations:
- Add a new to-do item
- Mark an item complete
- Delete an item

3. In Oracle Database Actions (SQL Web), run:

   ```sql
   <copy>
   SELECT * FROM todos_target;
   </copy>
   ```

4. Compare with your expected source footprint from Lab 4.

### 4. Validating and adjusting: Testing the output

Pass criteria:
- UI loads target data
- CRUD actions succeed without errors
- SQL results confirm target documents are present and coherent

[Optional] If discrepancies appear, re-run migration scripts from Lab 5 and repeat this sprint.

---

## Task 4: Sprint 3 — Explore AJD Benefits in 26ai

**Goal:** Explore key AJD platform capabilities now that the app is successfully running on the migrated target.

### 1. Planning: Crafting the prompt

*How to construct this prompt:* Ask for a practical, workshop-friendly walkthrough of key AJD value areas.

```text
<copy>
Final sprint: Sprint 3.

Please first provide a short plan only (do not execute actions yet). After I approve, execute the guided exploration.

Please give me a practical walkthrough to explore AJD benefits in Oracle AI Database 26ai for this migrated app, specifically:
- Security
- Scaling
- Monitoring
- AI features (including vector/semantic capabilities)

Include what I should click or check in OCI and one useful SQL example against `todos_target`.
</copy>
```

### 2. Reviewing the plan: Checking the AI's proposed implementation

Confirm the AI guidance includes:
- Security controls (encryption, ACL posture, auditability)
- Scaling behavior and operational simplicity
- Monitoring metrics to inspect
- AI-oriented exploration ideas relevant to JSON data

### 3. Acting on the plan: Allowing Cline to execute guided exploration

Toggle to **Act Mode** and let Cline execute the approved Sprint 3 exploration checklist.

1. **Security:** In OCI, review encryption defaults, access controls, and audit-related settings.
2. **Scaling:** Review auto-scaling options and capacity behavior.
3. **Monitoring:** Inspect metrics such as CPU and storage trends.
4. **AI in 26ai:** Review AI-related database capabilities relevant to document data and semantic workloads.

Run this SQL example:

```sql
<copy>
SELECT
    JSON_VALUE(DATA, '$._id') AS id,
    JSON_VALUE(DATA, '$.text') AS text,
    JSON_VALUE(DATA, '$.completed') AS completed
FROM todos_target;
</copy>
```

### 4. Validating and adjusting: Outcome check

Confirm you can:
- Explain at least one concrete benefit in each area (security, scaling, monitoring, AI)
- Query migrated JSON documents via SQL successfully

**Congratulations!** You have completed the end-to-end workshop lifecycle: build, analyze, migrate, validate, and explore advanced AJD capabilities on Oracle AI Database 26ai.

---

## Troubleshooting

- **No data in app after repoint:** Verify environment variables and restart the server in the same terminal session.
- **Data discrepancies:** Re-run migration from Lab 5 and compare counts before document-level checks.
- **SQL Web query issues:** Confirm you are connected to the correct AJD instance and user context.

---

## Acknowledgements

**Authors**
* **Luke Farley**, Senior Cloud Engineer, ONA Data Platform S&E

**Contributors**
* **Cline**, AI Assistant

**Last Updated By/Date:**
* **Luke Farley**, Senior Cloud Engineer, ONA Data Platform S&E, November 2025
