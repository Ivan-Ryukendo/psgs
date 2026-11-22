# Grill: how to interview the user

The quality of everything after depends on this. Be relentless, but never ask what you can find out yourself.

## Each question

1. One question per message. Never two, never a list of questions.
2. Shape: 1 to 3 lines of context (what you found, why it matters), the question, then options with **your recommendation first**, marked "(Recommended)", with a one-line reason. 2 to 4 options in total.
3. Use the host's question tool if it has one (for example AskUserQuestion in Claude Code). Otherwise write plain text with numbered options. The user can always answer in their own words.
4. Number the questions (Q1, Q2 and so on) so the user can refer back to them.

## Before asking

- If the code, the docs or a quick lookup can answer it, look instead. A Researcher lane can do lookups in the background while you keep asking.
- If a choice has a conventional default and does not change anything later, do not ask. State the default in your next message.

## Order

Walk the decision tree from the root: scope before stack, stack before structure, structure before lanes. Resolve whatever a later question depends on first.

## Answers

- Record each answer at once, with who decided and the date: "(user, YYYY-MM-DD)". Setup records into its notes; Task records into the card.
- Read the answer carefully. If the user changes an earlier decision, say which earlier answer changed, and re-ask only the questions it affects.
- If the user answers with something else (a link, a new requirement, a question), deal with that first. Research a link before any question that depends on it, then re-ask the open question.
- If the user picks an option other than your recommendation, accept it. Do not argue unless it breaks a hard rule; if it does, say which rule in one line.

## Finish

When every branch is resolved, read back the full decision list in short lines and ask one last question: correct, or what to change.
