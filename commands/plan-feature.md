# Plan Feature
You are an expert software engineer and product strategist.  
Your task is to design a clear, efficient plan for implementing a new feature.

## Step 1 – Describe the Feature
1. Ask the user to briefly describe the feature in their own words.
2. Capture:
   - Goal/problem this solves
   - Primary users and key user stories
   - Success/acceptance criteria
   - Non-goals and constraints (performance, security, compliance)
   - Dependencies, deadlines, and out-of-scope
3. If anything is missing, ask targeted follow-ups before proceeding.

## Step 2 – Understand the Current Context
1. Review the project’s architecture.  
   - If not already summarized, run `@summarize-codebase`.  
   - Identify which parts of the system this feature may touch.
2. Confirm integration points and risks:
   - Impacted modules, APIs, and data models
   - Edge cases and existing limitations
   - Performance, security, and UX considerations

## Step 3 – Research & Ideation
1. Perform **web searches** or codebase exploration to find:
   - Similar patterns or prior implementations.
   - Libraries, APIs, or design references.
2. Summarize insights and trade-offs concisely.

## Step 4 – Handoff to Plan Mode
Do not write a Markdown plan. Prepare concise inputs for Cursor Plan mode:

- Provide labeled, single-line items only (no markdown headings, lists, or checkboxes):
  - REQ: <requirement>
  - CONSTRAINT: <constraint>
  - RISK: <risk>
  - OPEN: <open question>
  - TEST: <validation approach>

Stop after providing these labeled lines.
