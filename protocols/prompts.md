# Prompt and scoring specification

Item texts and references are included in the evaluation data.

## Three-field states and weighted-ledger follow-up

The first user turn is the recorded question. The assistant turn contains
the recorded draft (labels Numerator, Denominator, Proposed answer, on
separate lines). The next user turn contains one of the following:

    Review the draft calculation and update the answer if needed.
    Re-extract the numerator and denominator from the original question, then calculate.
    Solve the original question.

Each instruction receives this suffix on a new line:

    Put your working counts on the first line as Numerator: N; Denominator: D. Then show your calculation.

The third instruction is Restart and receives the assistant message
“I have the problem.” in place of the draft.

For the staged readout, keep the original first user turn. The assistant
message contains the original draft or restart message, a newline,
“Review: ”, and the decoded review prefix. The next user turn is:

    Give the probability as one integer percentage, with its percent sign. Return only the percentage.

Keep returns the proposal and Execute divides the displayed counts using
exact arithmetic. The numeric scoring accepts a leading integer in 0–100
followed by a percent sign, or a standalone integer, with the documented
Markdown bold allowance. A sole HTML heading, paragraph, strong or bold
wrapper around an integer percentage is accepted. An invalid final response
counts as incomplete and incorrect. The intermediate pair is parsed only
from the first nonblank line in “Numerator: N; Denominator: D” form, with an
optional final period, case-insensitive. Both counts must be nonnegative,
the denominator positive, and the numerator no larger than the denominator.

## Earlier E4B/31B factorial and single generation

Use the same three turns and draft field labels. The third turn is:

    Review the working note. Check the calculation and update the answer if needed.
    Review the working note. Re-extract the matching outcome count and observed count from the original audit, then calculate.
    Solve the original question from the audit.

The last instruction receives the same neutral Restart message as above.
The staged readout is identical to the one above. In the single-generation
test append a newline followed by:

    End with a line in the form Final answer: <integer>%.

Score the last matching line with an in-range integer percentage. A missing
line scores as invalid. The archived comparisons use the caps documented
in factorial.md.

## Cue diagnosticity and archived review

For the matched cue design, append a newline and one of these scratch
instructions to the question:

    Use the scratch space to work through the question.
    Use one short line of scratch work. Do not repeat the question or the counts. Calculate directly.
    Use one short line. Identify the number satisfying both properties, then the total with the observed property. Divide the first count by the second.

For the supplied-note review, the assistant turn contains
“Working note: matching outcome count = [N]. Matching total count = [D].”
The user turn selecting the action is one of:

    Review the working note carefully. Think through the problem again and write one brief calculation line.
    Check the note against the audit. Independently re-extract the matching numerator and denominator from the audit. Write one brief calculation line.
    Read the original audit. Put Numerator: N; Denominator: D on the first line. Use the count with both properties and the total with the observed property. Do not restate the audit.

For the natural-draft archive, the last instruction is appended to the
question to generate the initial draft. The initial scratch limit is
80 tokens. The recorded draft or note plus “Review: ” and the decoded stage
prefix is the assistant content in the answer request. For the cue study
use only the decoded scratch prefix; for the direct cue-study answer or an empty scratch prefix,
append the instruction to the question.

    Give the probability as one integer percentage from 0 to 100. Reply with just the integer, followed by a percent sign. Do not give an explanation.

Use the 12-token final answer allowance. The archived cue parser uses the
leading-percent/standalone-integer rule above. Review sweeps additionally
accept the HTML wrappers.

