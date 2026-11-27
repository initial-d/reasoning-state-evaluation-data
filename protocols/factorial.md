# Reasoning state repairability experiment

Frozen before factorial inference. The E4B screen and the 31B confirmation
use separate questions. The unit of analysis is one question per scenario group.

## Design and outcomes

- E4B screen: 48 questions. Random priority over the archived E4B scenario
  groups, one prompt per group, with no selection on the model's outcomes.
  Replay the archived natural draft on each selected question as well.
- Conditional confirmation: 72 new questions from the existing count-table
  generator (seed 201367), excluding scenario signatures already seen in the
  archival studies. Use the first eligible groups in generator order.
  Run Gemma 4 31B on the same factorial menu under the staged protocol and
  a single-generation protocol. Use all eligible groups up to the stated
  fixed count; abort if the candidate pool cannot supply that count.
- On each question, cross exact versus wrong source operands with correct
  versus wrong proposed answer. Use the other outcome count in the observed
  slice as the wrong numerator. Draw the wrong percentage from a seeded
  list of ±5 and ±10 changes, excluding the correct answer and the value
  implied by the wrong operands. All four draft variants have the same
  wording and token count for both review prompts. Record the four realized
  prompt lengths. Eligibility is computed before model generation.
- Correct process means the two certified source counts are exact. The
  draft contains the counts and a separately labeled answer, with no
  extra derivation that states the ratio. The wrong/wrong cell tests a
  wrong answer distinct from both ratios. It does not represent a
  coherent derivation with a wrong premise.
- Cross Keep, Execute, Generic Review, Source Review, and Restart with
  review caps of 64 and 320 tokens. Keep and Execute are deterministic and
  identical across budgets. Execute uses only visible operands and falls
  back to Keep when those operands cannot be parsed. Restart replaces the
  draft with a neutral assistant turn and is shared across factorial
  cells. Review instructions receive the draft in the same assistant
  role. No label, gold check, or error locator is passed to any action.
- The staged protocol uses prefixes of a single 320-token review and a
  separate 16-token answer request. The normal protocol generates the
  review and a required final-answer line in a single assistant turn,
  with total caps of 80 and 336. Invalid readouts score as incorrect
  and are tabulated separately. Retain every action and cell.

## Analysis and stopping rule

The primary estimand at a 320-token review cap is
`(Source − Generic | wrong process) − (Source − Generic | correct process)`,
averaged equally over the two proposed-answer states. Estimate it as a
mean of question-level interaction scores. Report two-sided percentile
95% paired intervals from 20,000 question bootstrap draws, seed 81317.
The E4B screen triggers the single 31B confirmation only if the absolute
point estimate is at least 10 percentage points and at least 85% of its
bootstrap scores have its sign. The screen is exploratory. On 31B, the
staged estimand is the sole primary replication test. Report the point
estimate and interval even if the sign changes or the interval crosses
zero. Report the single-generation replication as a protocol sensitivity
check, with the same estimand and analysis.

Secondary analyses use the same paired bootstrap and are descriptive:
the primary contrast at 64 tokens, its 320-minus-64 interaction, the
answer-status interaction, individual action/cell accuracies,
valid-answer rates, and repair/regression relative to Keep.

For the archive, parse only unambiguous labeled operand pairs. Compare
each count against the original table to distinguish numerator,
denominator, joint, answer-only, and unscorable states. Record whether
an incorrect answer matches the emitted ratio and whether a wrong pair
implies the correct ratio. Keep format failures separate from wrong
numeric answers. Rescore archived review results by type and report
sample sizes. On the paired E4B screen questions compare the naturally
generated draft with the factorial cell matched by verified process
and answer status wherever both are scorable. This difference includes
stylistic and severity differences and is descriptive.

Gold labels define the interventions and the offline strata. Every
action is evaluated in every manufactured state, and neither the
action prompt nor the executor queries the states' gold labels.
No policy selects an action using the strata, so these experiments
estimate repairability rather than routing performance.
