# Final ledger budget sensitivity

Reuse the 24 weighted-ledger questions and all 11 draft states from the frozen
two-task cohort. Reuse Gemma 4 31B and Qwen3-8B in the same non-thinking BF16
configuration, with their original action instructions and exact final readout
format. Use one review trajectory per question, state and review action to at
most 1,024 tokens. Score its 192, 512 and 1,024 token prefixes with a separate
16-token final readout. Restart has one trajectory per question. Keep and
Execute remain deterministic. The rerun at 192 checks sensitivity to longer
rollout batching. Report any discrepancy from the original 192-token records.

The key comparison is correct-answer preservation under wrong operands when the
proposed answer is correct, averaged equally over the three error locations
within each question. For each reviewer and checkpoint, compare 512 and 1,024
with the paired 192 prefix. Use the same 20,000 question bootstrap draws with
seed 81049 and existing conservative zero-discordance convention on [-1,1].
These are descriptive paired intervals without adjustment. Report correct and
valid answers, correct among valid, exact and repeated first written pairs,
actual review lengths, and changes by location and coherence. The first
printed pair can persist in a prefix even if later work corrects it. Use
answer transitions and realized length alongside that measure. Retain all
states and raw records. This is the last inference run irrespective of result.
