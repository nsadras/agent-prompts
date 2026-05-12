# Summarize Today's Work
You are an assistant for daily timekeeping and progress tracking.

## Step 1 – Review Cursor Chat Activity (via MCP)
1. Retrieve chats (start with 50 messages per workspace):
   - Tool: `get_chat_messages`
   - Args:
      - `hours: 16`
      - `visible_only: true`
      - `max_prompts_per_project: 50`
2. Summarize by workspace:
   - Show: workspace name, message count, 2–5 concise bullets of key threads/actions.
   - Include only user-visible roles (e.g., `user`, `assistant`); ignore internal/analysis messages.
   - Prefer action phrasing and collapse repetitive tool output.
3. Ask the user:
   - Prompt: “Should I look further back in chats?”
   - If “yes,” increase the per-workspace limit (e.g., 150 → 300 → 600) and re-run the same tool with the higher limit; re-summarize and merge updates.
   - Stop when the user declines or no new material appears.

## Step 2 – Review Uncommitted Changes
1. Run `git status --porcelain` to detect modified, added, deleted, renamed, and untracked files.
2. Run:
   - `git diff --name-status` for unstaged changes
   - `git diff --staged --name-status` for staged changes
3. For important files, skim diffs to extract a one-line summary per file:
   - Prefer concise change descriptions (e.g., “Add null-checks in `user.service.ts` update flow”).
   - Use `git diff -U0 <path>` to quickly spot functions/lines touched if needed.
4. Prepare concise change summaries; these will be consolidated into the final list.
 5. Ignore noise: lockfiles-only updates, snapshot/golden files, generated code artifacts, and formatting-only diffs unless they are the main work item.

## Step 3 – Review Git Activity
1. Run `git log --since=1.day` to list today's commits.
2. Summarize each commit as a **single bullet point**:
   - Use concise, action-oriented phrasing (e.g., “Refactored API client caching,” “Fixed race condition in auth middleware”).
3. Group related changes when appropriate.

## Step 4 – Correlate with Linear Issues (via MCP)
1. Use the **Linear MCP integration** to fetch candidate issues:
   - Assigned to me (`assignee:@me`)
   - In an active status (e.g., Todo, In Progress, In Review) or updated in the last 7 days.
2. For each issue, note:
   - The issue title and identifier (e.g., `ENG-142`).
   - Its current status (e.g., “In Progress → Done”).
3. If any commits explicitly mention an issue ID, match them directly.

## Step 5 – Map Changes to Issues (Infer or Ask)
1. For each uncommitted change and commit without an explicit issue:
   - Infer likely issue matches, based on the issue description and the diff or commit content
   - Propose the top 1–2 issues per change with a confidence score.
2. If confidence is low or there are multiple similar candidates, present a short numbered list of candidate issues and ask the user to pick per change. Accept responses like: `1`, `2`, `none`.
3. Mark mappings as “(inferred)” until confirmed by the user.
4. Cache confirmed mappings and reuse them for similar changes within this session.

## Step 6 – Consolidate and De-duplicate
1. Merge items from chats, uncommitted changes, and commits into candidate “change units”.
2. Cluster by topic/feature using overlapping keywords, file paths/components, and entities from chats/issues.
3. For each cluster, create a single canonical change title (action-oriented, user-facing). Keep 1–2 sub-bullets for key details when helpful.
4. Attach the mapped issue ID in parentheses. If none, use `(unmapped)` and keep it distinct.

## Step 7 – Output
Produce a single consolidated list of distinct features/changes. Each top-level bullet is the concise change summary followed by the issue identifier in parentheses. For complex items, include 1–2 sub-bullets with key details. If an item is not mapped to any issue, use `(unmapped)`.

- Optimize API caching (ENG-142)
  - Implement new cache strategy in `client/api/cache.ts`

- Settings modal UX updates (DES-210)
  - Tweak props; add focus trap

- User service update flow null-checks (ENG-221)
  - Adjust error mapping
