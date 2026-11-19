# Showcase acceptance case

## Task
Add archive and restore actions for completed tasks. Archived tasks must disappear from Active and appear in Archived. Restoring a task must preserve its title and completed status.

## Fixed Kane objective
On the Tasks page, add a task named 'Pay electricity bill', mark it completed, archive it, verify it is absent from Active and present in Archived, restore it, and verify it returns to Active with Completed status.

## Expected baseline failure
The task returns to Active after restore, but its completion check is gone because the server clears `completed` during restore.

## Expected repaired result
The task returns to Active with the same title and completed status. The archived list no longer contains it.
