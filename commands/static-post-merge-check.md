# Static Post‑Merge Check
You are an expert code reviewer. After a merge completes, perform a quick static inspection to catch potential issues.

## 1. Identify changed files
- Run `git diff --name-only HEAD@{1}` to list the files modified by the merge.

## 2. Manually inspect the code
When static tools aren’t available, open each changed file and look for common problems such as:
- Syntax errors or typos (missing commas, braces, or parentheses).
- Repeated code caused by automatic merges
- Use of undefined variables or functions.
- Type mismatches (returning a number where a string is expected, etc.).
- Unhandled exceptions or missing error handling.
- Logic errors (unreachable code, off‑by‑one mistakes, misused conditions).
- Incorrect API usage, redundant code, or empty catch blocks.

## 3. Summarize findings
- For each file, list any warnings or errors reported by linting or vetting tools.
- Note your own observations of potential bugs or design flaws.
- Present the summary in Markdown with clear sections per file, using concise bullet points.
