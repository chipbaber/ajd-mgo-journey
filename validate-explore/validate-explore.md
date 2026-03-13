# Lab 6: Validate and Explore AJD Benefits

## Introduction

In this lab, you'll repoint your To-Do application to the migrated target collection in AJD, validate the functionality and data integrity, and explore AJD's benefits like security, scaling, monitoring, and AI features in Oracle AI Database 26ai. This confirms a successful migration with enhanced capabilities.

> **Estimated Time:** 15 minutes

**Note:** AI-generated output is non-deterministic. The instructions below first provide prompts for you to run in Cline and review the results. If you are not happy with the generated output, use the manual `[Optional]` steps in each task to complete the lab with the tested workflow.

---

### Objectives

In this lab, you will:
- Learn and experiment with using Cline to validate the migrated application
- Repoint the app to the target collection
- Validate application functionality and data integrity
- Explore AJD benefits: security, scaling, monitoring, and AI integration in 26ai

---

### Prerequisites

This lab assumes you have:
- Completed Lab 5
- The To-Do app from Lab 3
- Migrated data in 'todos_target'

---

## Task 1: Repoint the Application to Target Collection

1. In your terminal, navigate back to your app directory:

   ```bash
   <copy>
   cd path/to/todo-app
   </copy>
   ```

2. Ask Cline to confirm which environment variables need to change so the application points at the migrated target collection.

```bash
add prompt: Ask Cline which environment variables need to change to point the To-Do app from the source AJD collection to the migrated target collection.
```

*add image: Cline response explaining the required `SOURCE_MONGO_API_URL` and `COLLECTION_NAME` updates.*

3. Update the environment variable to point to the target AJD instance.

   **Recommended:** keep the collection name the same on the target (e.g., still `todos_source`) so the application only needs the URI changed.
   
   ```bash
   <copy>
   export SOURCE_MONGO_API_URL="$TARGET_MONGO_API_URL"
   export COLLECTION_NAME='todos_target'
   </copy>
   ```

   If you kept the same collection name on the target, you can omit `COLLECTION_NAME` entirely.

   **Note:** This changes the connection from the source to the target AJD instance. For real MongoDB to AJD migrations, typically only the URI changes—no code edits needed, as AJD is compatible. Collections can remain the same or be specified via env for flexibility. If needed, update server.js to use process.env.SOURCE\_MONGO\_API\_URL accordingly.

[Optional] Use the export commands above manually if you do not want to rely on the Cline output.

4. Restart the server:
   ```bash
   <copy>
   node server.js
   </copy>
   ```

*add image: Terminal showing the updated environment variables and the restarted app server.*

---

## Task 2: Validate Application Functionality

1. Ask Cline for a short validation checklist to confirm the migrated application is working correctly.

```bash
add prompt: Ask Cline for a short validation checklist to confirm the migrated tasks load correctly and CRUD still works after repointing the app.
```

*add image: Cline response listing the migration validation checklist.*

2. Open `http://localhost:3000` in your browser. You should see the migrated tasks from `todos_target`.

![Migrated Tasks](./images/migrated-tasks.png)

3. Test CRUD operations:
   - Add new to-do items.
   - Complete and delete items.
   - Ensure the migrated data appears correctly.

4. Verify data integrity:
   - In Oracle Database Actions, run:
     ```sql
     <copy>
     SELECT * FROM todos_target;
     </copy>
     ```
   - Compare with source data in todos_source from Lab 4.

*add image: SQL Web showing `SELECT * FROM todos_target;` results for validation.*

[Optional] Validate manually by confirming the migrated tasks load in the UI, CRUD operations still succeed, and the rows in `todos_target` match the expected migrated data.

---

## Task 3: Explore AJD Benefits

1. **Security:** In the Oracle Cloud Console, review AJD's automatic encryption, ACLs, and audit logging.

2. **Scaling:** View auto-scaling options in the database details—AJD automatically handles workload spikes.

3. **Monitoring:** Check performance metrics (e.g., CPU, storage) in the console for insights.

4. **AI Features in 26ai:** Explore integrated AI capabilities like vector search for semantic queries or ML models for data insights directly in the database.

### Example: Query JSON documents using SQL

```sql
<copy>
SELECT
    JSON_VALUE(DATA, '$._id') AS id,
    JSON_VALUE(DATA, '$.text') AS text,
    JSON_VALUE(DATA, '$.completed') AS completed
FROM todos_target;
</copy>
```

[Optional] Review the AJD console manually and run the SQL example above to inspect the migrated JSON documents from SQL.

**Congratulations!** You've completed the end-to-end journey: building, migrating, and scaling on Oracle AI Database 26ai.

---

## Troubleshooting

- **Data Discrepancies:** Re-run migration if issues; verify with queries.
- **Performance:** Ensure optimal indexing; AJD manages many aspects automatically.

---

## Acknowledgements

**Authors**
* **Luke Farley**, Senior Cloud Engineer, ONA Data Platform S&E

**Contributors**
* **Cline**, AI Assistant

**Last Updated By/Date:**
* **Luke Farley**, Senior Cloud Engineer, ONA Data Platform S&E, November 2025
