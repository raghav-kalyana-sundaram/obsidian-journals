# Working with AI Models: A Guide to Implementing Detailed Steps

How to effectively use Claude Code, ChatGPT, or other AI models to implement the plugin using the detailed step descriptions (no code included).

---

## Overview

You have detailed descriptions of what needs to be built (20 steps). You'll use an AI model to write the actual code. This guide explains how to communicate effectively with AI to get high-quality results.

---

## Philosophy

**Your role**: Architect and QA. You understand what needs to be built, you validate that it works, you decide what's acceptable.

**AI's role**: Implementation. Write the code, fix bugs, optimize, refactor.

**The workflow**: You describe what's needed, AI writes code, you test and iterate.

---

## Communication Patterns

### Pattern 1: Implementing a New Feature

**You should say:**
"Step 8 requires implementing an entry creation command. Here's what needs to happen:
- Update the main plugin file to add a create entry command
- When user clicks the ribbon icon, retrieve the default journal from settings
- Call the journal manager to create a new entry
- Show a success notification
- Open the newly created file

Can you implement this?"

**What NOT to say:**
- Don't include code examples (unless you want the AI to follow that pattern exactly)
- Don't say "just like the X feature" (unless you've shown the feature)
- Don't ask to "simplify" without explaining what that means

**What the AI will do:**
- Write the implementation based on the existing code structure it has seen
- Integrate with the journal manager you've already built
- Follow the patterns established in previous steps
- Return code ready for testing

---

### Pattern 2: Fixing a Bug

**You should say:**
"When I create an entry, it says 'success' but the file doesn't appear in the vault. The journal folder exists. What's wrong?"

**Provide context:**
- What were you trying to do
- What happened instead
- What error messages appeared (if any)
- What did you check already

**What NOT to say:**
- "It's broken" (not helpful)
- "Fix the bug" (AI needs details)
- "I think the problem is..." (unless you're confident)

**What the AI will do:**
- Ask clarifying questions if needed
- Examine the code flow to find the issue
- Suggest fixes and test them
- Explain what went wrong and why

---

### Pattern 3: Understanding Design Choices

**You might ask:**
"Step 7 says to cache entry queries. Why is this important? When should the cache be invalidated?"

**What the AI will explain:**
- Why caching helps (performance)
- When it matters (large vaults)
- How to invalidate it (when new entries are created)
- Trade-offs (slightly stale data vs. fast loads)

---

### Pattern 4: Extending or Customizing

**You should say:**
"Step 3 includes five built-in templates. Can I easily add more templates? Walk me through how I'd do that without breaking anything."

**What the AI will do:**
- Show you the extension points
- Explain how to add new templates safely
- Warn you about any dependencies or side effects
- Provide guidance on testing changes

---

## Session Structure

A typical session working with an AI model should follow this pattern:

### 1. Preparation (5 minutes)
- Open the detailed steps guide
- Pick the step you're implementing
- Read it carefully
- Note any dependencies on previous steps
- Understand what success looks like

### 2. Briefing (5 minutes)
- Tell the AI which step you're working on
- Paste or describe what needs to happen
- Explain what files need to be created or modified
- Point out any integrations with existing code

### 3. Implementation (15-20 minutes)
- AI writes the code
- You review it
- Ask questions about parts you don't understand
- Request changes if something doesn't feel right
- Iterate until it matches the spec

### 4. Integration (5 minutes)
- AI helps you integrate the new code with existing code
- Makes sure imports and dependencies are correct
- Ensures no conflicts with previous work

### 5. Testing (5-10 minutes)
- You test the feature
- Tell the AI the results
- If it doesn't work, provide specifics about what failed
- AI fixes issues

### 6. Iteration (varies)
- Keep testing until everything works
- Polish and optimize if needed
- Get ready to commit

### 7. Git Commit (2 minutes)
- Use the suggested commit message from the step guide
- Commit your changes

---

## What to Prepare Before Each Session

**Have ready:**
- The detailed steps document open
- The current step clearly identified
- Existing code files (so AI understands the structure)
- Your test vault running (Obsidian open, ready to test)
- Two terminals or windows: one for code, one for testing

**Know:**
- What step you're on
- What the last working step was
- What you need to test
- What success looks like for this step

---

## How to Ask for Code

### For a brand new file:
"Create the file [path/filename.ts] that does the following:
- [requirement 1]
- [requirement 2]
- [requirement 3]

It needs to integrate with [existing component]. Here's what that component looks like:
[brief description of integration point]"

### For modifications to existing file:
"In [path/filename.ts], update the [function/class name] to:
- [change 1]
- [change 2]

This is for Step [number]: [brief description of what we're implementing]"

### For a refactor:
"Can you refactor [existing code] so that:
- [goal 1]
- [goal 2]
- [goal 3]

The current behavior should stay the same, but the code should be [cleaner/more modular/etc.]"

---

## Error Handling in Communication

### When AI Makes a Mistake:

**Don't:**
- "This is wrong"
- "That doesn't work"
- "Just fix it"

**Do:**
- "I tried this code and got error: [exact error message]"
- "This doesn't work because [what you observed]"
- "I expected [what should happen] but got [what happened]"

### When You Don't Understand Something:

**Don't:**
- "Explain this better"
- "Why did you do this?"

**Do:**
- "I don't understand how this [specific part] works. Can you walk me through it?"
- "Why did you choose [approach] instead of [alternative]?"
- "Can you point out where [concept] is implemented?"

---

## Quality Checkpoints

After the AI implements each step, before you test, check:

**Does the code:**
- [ ] Follow the pattern of existing code (naming, structure)?
- [ ] Have clear comments on complex logic?
- [ ] Handle errors gracefully (try-catch where needed)?
- [ ] Integrate cleanly with existing components?
- [ ] Include all required functionality from the step?
- [ ] Not duplicate code that already exists?
- [ ] Not break existing functionality?

**If any of these are no, ask the AI to fix it before testing.**

---

## Testing Collaboration

### When You Test:

**Report good news:**
"I tested Step 8 and everything works! Entry creation works, success notification appears, file opens automatically. Ready to move to Step 9."

**Report problems:**
"I tested Step 8. The entry was created but it didn't open automatically. No error in console. The folder exists and is at [path]. What should I check?"

**Report partial success:**
"Most of Step 8 works. Entry creation works and opens. But the success notification doesn't appear. Is that expected?"

### When Testing Fails:

**Provide:**
- What you tried to do
- What happened instead
- Any error messages (exact text)
- Console logs (if relevant)
- What folder/file structure looks like (if it's a file system issue)
- Whether previous steps are still working

**Example:**
"I'm on Step 9. When I create an entry with mood auto-capture enabled, no mood selector appears. The console shows: [paste error]. In settings, mood auto-capture is enabled. Do I need to do something else?"

**Let the AI ask clarifying questions if needed.**

---

## Iterating on Implementation

If the first implementation doesn't quite match what you need:

**Step 1: Identify the gap**
"The template rendering works, but variables aren't being replaced. For example, {{date}} shows as {{date}} instead of 2025-01-07."

**Step 2: Ask for clarification**
"Is this because the template variable matching is case-sensitive? Should it be case-insensitive?"

**Step 3: Request the fix**
"Can you update the variable replacement to handle both {{date}} and {{DATE}}?"

**Step 4: Test again**
"Tested again. Now {{date}} works but {{location}} shows empty. Should it show 'Location: [value]' or just '[value]'?"

---

## Working Across Multiple Steps

### Maintaining Context:

The AI might not remember what you built in previous steps. Help it:

"I've completed Steps 1-7. I'm now on Step 8. Here's what I have so far:
- [brief description of each completed step]
- [current state of the code]

For Step 8, I need to [requirement]. Can you implement this while maintaining compatibility with what I've built?"

### Showing Examples:

If you want the AI to follow a pattern from previous steps:

"In Step 4, I implemented plugin lifecycle like this: [describe what you did]. For Step 11, I want to follow the same pattern for the calendar view. Can you implement it similarly?"

---

## When to Ask for Explanation

### Ask for explanation when:
- Something in the code is unclear to you
- You want to modify something but don't know where to start
- You're about to make a commitment (commit to Git) and want to understand what you're shipping
- You're curious about a design choice

### Good questions:
- "Walk me through how [feature] works from user action to file creation"
- "Why did you use [approach] instead of [alternative]?"
- "If I wanted to add [new feature], where would I add it?"
- "Can you explain what this section does in plain English?"

---

## Pacing and Breaks

### Recommended Session Structure:

**Total development time: ~8 hours across multiple sessions**

**Option 1: Weeklong pace (1 hour per day)**
```
Monday: Steps 1-2 (1 hour)
Tuesday: Steps 3-4 (1 hour)
Wednesday: Steps 5-7 (1.5 hours)
Thursday: Steps 8-10 (1.5 hours)
Friday: Steps 11-14 (2 hours)
Weekend: Steps 15-20 (1.5 hours)
```

**Option 2: Weekend intensive (3-4 hours per day)**
```
Saturday: Steps 1-10 (4 hours)
Sunday: Steps 11-20 (4 hours)
```

**Option 3: Weeklong focused (2 hours per day)**
```
Monday: Steps 1-4 (2 hours)
Tuesday: Steps 5-7 (2 hours)
Wednesday: Steps 8-10 (2 hours)
Thursday: Steps 11-14 (2 hours)
Friday: Steps 15-20 (2 hours)
```

### Between Sessions:
- Commit your work to Git
- Test one more time to make sure everything is stable
- Note what's next (Step N+1)
- Close everything and take a break

---

## Decision Making During Implementation

### When the AI suggests an alternative approach:

**Evaluate based on:**
- Does it still meet the step requirements?
- Is it simpler or more complex than described?
- Does it integrate well with existing code?
- Is the trade-off worth it?

**Examples:**
- If AI suggests using a library to replace 50 lines of code, evaluate if the dependency is worth it
- If AI suggests a different data structure, evaluate if it makes the code clearer
- If AI suggests performance optimization, evaluate if it's needed now or later

### When you need to deviate from the steps:

**Get AI input:**
"The steps say to do [X], but I'm thinking of doing [Y] instead because [reason]. What are the trade-offs?"

**Get feedback:**
- Pros and cons of each approach
- Impact on future steps
- Difficulty of reverting the decision

---

## Working with Multiple AI Models

If you switch between Claude, ChatGPT, or other models:

**Give context every time:**
"I'm building an Obsidian plugin. I've completed steps 1-7. Here's what I have: [brief overview]. I'm now working on Step 8. Here's what needs to happen: [requirements]."

**Show existing code:**
"Here's my journal manager from Step 7: [brief description of what it does and key methods]"

**Be explicit about requirements:**
"I need Step 8 to integrate with the journal manager without breaking it. The new code should add a command and ribbon icon that call the journal manager's create entry function."

---

## Quality Control Checklist

Before moving to the next step, verify:

**Functionality:**
- [ ] Feature works as described in the step
- [ ] No console errors
- [ ] Integration with previous steps works
- [ ] All error handling is in place

**Code Quality:**
- [ ] Code follows the pattern of existing code
- [ ] Comments explain complex logic
- [ ] No obvious performance issues
- [ ] No code duplication

**Testing:**
- [ ] Manual testing passed
- [ ] Tested in both light and dark mode
- [ ] Tested on different window sizes (if UI involved)
- [ ] Tested error cases (if applicable)

**Documentation:**
- [ ] Current step documentation is accurate
- [ ] Code changes are understandable
- [ ] Ready to commit to Git

**If any check fails, iterate with the AI until it passes.**

---

## Troubleshooting Common Issues

### "The code doesn't compile"
- Ask the AI: "I'm getting this error: [paste error]. Can you fix it?"
- Provide context: "I'm using [version] of TypeScript"
- Ask for explanation: "Why did this happen?"

### "It compiles but doesn't work"
- Describe what should happen vs. what happened
- Ask the AI to review the logic
- Consider the integration points
- Test smaller pieces in isolation

### "It works but I don't understand why"
- Ask the AI to explain each step
- Ask for comments in the code
- Ask for a conceptual walkthrough
- Don't move forward until you understand it

### "It works but feels wrong"
- Trust your instincts
- Ask the AI: "Is there a cleaner way to do this?"
- Ask about alternatives
- It's okay to refactor before moving on

---

## Success Indicators

You're doing this right if:

✅ Each step takes the estimated time (20 min to 1 hour)
✅ You understand what was built and why
✅ Code integrates smoothly with previous steps
✅ Testing reveals minimal issues
✅ You can explain the feature to someone else
✅ Git history shows clear, meaningful commits
✅ You're excited about the progress

---

## When to Ask for Help vs. Iterate

### Ask for help when:
- Something consistently doesn't work and you've iterated 3+ times
- You're fundamentally confused about a concept
- You want to understand design trade-offs
- You need technical guidance on Obsidian API

### Iterate on your own when:
- Small tweaks are needed (spacing, colors, edge cases)
- You're just testing to find the issue
- You understand the problem and have a solution in mind

---

## Final Reminders

1. **Take breaks** - You're making architectural decisions. Mental freshness helps.
2. **Test thoroughly** - Don't assume it works. Verify each step.
3. **Understand what you're building** - You own this code. Know it.
4. **Commit often** - Don't let changes pile up. Commit after each working step.
5. **Ask questions** - Good communication with AI produces better results.
6. **Celebrate progress** - You're building something real. Take pride in it.

---

## Example Session

Here's what a real session might look like:

**You:** "I'm on Step 8. I need to add an entry creation command. When the user clicks the ribbon icon, it should get the default journal, call the journal manager to create an entry, show a success notification, and open the file. Here's my current main.ts: [show relevant parts]."

**AI:** "I'll update main.ts to add the create entry logic. Let me create the function and wire it to the ribbon icon."

**AI:** [shows code]

**You:** "This looks good. Let me test it." [you build and test in Obsidian]

**You:** "It works! Entry was created and opened. One question—in the createNewEntry function, where does the mood get passed to the journal manager?"

**AI:** "Good question. Currently it's not. For Step 9, we'll add the mood selector modal. The mood will be captured there and passed to journal manager."

**You:** "Makes sense. Committing this now: 'feat: add create journal entry command and ribbon icon'"

**Next:** "Let's move to Step 9. I need to implement the mood selector..."

---

This is the rhythm you'll establish: Read → Brief → Implement → Test → Understand → Commit → Move On

You've got this! 🚀
