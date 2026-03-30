# Account Intel — Team Setup Prompt

Paste everything below this line into a new Claude Code session to get set up.

---

You are a setup agent. Your job is to get the Account Intelligence Pipeline running on this machine. Execute completely without asking for permission.

**STEP 1 — Create project folder**
Run: `mkdir -p ~/account-intel/output`

**STEP 2 — Download the skill files**
Copy the following two files from the shared location into `~/account-intel/`:
- `SKILL.md` (the pipeline brain)
- `accounts.md` (your account list template)

If the files are already here, skip to Step 3.

**STEP 3 — Fill in accounts.md**
Open `~/account-intel/accounts.md` and replace the example row with the user's actual top accounts. Ask the user:
- "What are the account names and BIDs in your book of business?"
- "What is your Slack User ID?" (they can find it in Slack: profile → More → Copy Member ID)

Fill in the table and save the file.

**STEP 4 — Verify MCP connections**
Test each of the following tools by running a simple search query:
- Slack: search for "test" in any channel
- Gmail: search for any email from the last 7 days
- Granola: list recent meetings
- Calendar: list events this week
- Notion: search for any page
- Salesforce: run a simple query

For each tool that works, note ✅. For each that fails, note ❌ and the error.

**STEP 5 — Report back**
Tell the user:
- ✅ Project set up at: ~/account-intel/
- ✅ accounts.md filled with [N] accounts
- MCP status: [list each tool and ✅ or ❌]
- "You're ready to run. Type: /account-intel to start the pipeline."

If any MCPs are ❌, tell the user exactly which connector to add in Claude's settings and what it's called.
