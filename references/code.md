# Code module (draft, untested)

Slot = real names and one non-negotiable constraint.

## Code tells (audit only)
- Comments that narrate the next line ("# Loop through the list").
- Banner docstrings on trivial functions.
- Generic names: data, result, temp, handle_x, process_data, helper.
- A try/except around everything, catching broad exceptions and logging "An error occurred".
- Config, classes, or abstraction layers nothing needs yet.
- READMEs with emoji headers, "🚀 Features", or "robust, scalable, seamless".
- Print or log lines with checkmark emoji.

## Moves
- Name things after the domain he gave.
- Comment only on why, and only where the why isn't obvious.
- Handle the errors that can actually happen, and let the rest raise.
- Write the smallest version that meets the constraint.
- README: what it does in one sentence, how to run it, one known limitation.
