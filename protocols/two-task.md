# Final repairability experiment

Freeze this specification before inference. Run once on Gemma 4 31B IT
and Qwen3-8B in non-thinking mode. Use the same 24 generated questions in
each of two task families on both checkpoints. Seed 671239; choose the
first candidates with distinct, integer, two-digit ratios and matching
tokenized prompt lengths on both checkpoints. Failure to obtain this
cohort stops the experiment before inference.

The tasks are conditional count selection and a multistage weighted
ledger (classify rows, apply capped debits, multiply by tier weight, sum
eligible rows). The question asks for an exact integer percentage.
The displayed state supplies two accumulated operands and a proposal.
The numerator distractor is the other outcome count or the corresponding
weighted ledger total. The denominator distractor includes ineligible cases and is twice
the eligible total. The reference and three corrupted pairs give distinct integer
percentages. For each exact pair show the reference or one wrong
proposal. For each corrupted pair cross a correct proposal, the wrong
percentage implied by that pair, and a wrong proposal equal to the
ratio of the next corrupted pair in a fixed cyclic order. This keeps
the multiset of wrong proposed values fixed across corrupted pairs
while varying their agreement with the displayed calculation. Within an
error type the coherent and conflicting proposals can differ in distance
from the reference, so location-specific coherence effects include the
numerical substitution.

Evaluate Keep, Execute, Generic Review, Source Review, and Restart.
Both review instructions request the same first line with the working
numerator and denominator. Only Source requires fresh extraction from
the question. Use staged budgets of 64 and 192 review tokens with a
separate 16-token final readout. Both prefixes derive from the same
192-token review. Use greedy BF16, and retain raw work, raw numeric
readouts, prompt lengths, and actual output lengths. Score the working
pair only if the first nonblank line can be parsed as two nonnegative
counts with a positive denominator. Label parse failures separately.
Gold construction and offline scoring remain independent of prompts.

Primary outcome on multistage tasks at 192 review tokens: Source
minus Generic accuracy for corrupted pairs minus the same gap on exact
pairs, holding the proposed answer correct, with equal weighting of
three corruptions. Test each checkpoint using a paired question-level
two-sided sign-randomization test (100,000 draws, seed 81049); adjust the
two checkpoint tests using Holm. This test assumes sign exchangeability
under the null. Report a paired percentile 95% interval (20,000 draws,
seed 81049); when the bootstrap interval is a point, report a
conservative symmetric interval around the point using a one-sided
exact 95% upper bound for observing a departure in the remaining
questions conditional on the first question and the largest
possible absolute departure on the contrast's known support. The
conditional-count cohort is a descriptive task comparison.

Secondary, descriptive: all state/action outcomes; same contrast at
64 tokens and on the count task; operand-location and budget
differences; coherent versus conflicting wrong proposals; retention of
an edited pair and recovery of the exact pair among all reviews,
including a separate unknown-pair category; answer repair (given
wrong initial answer), regression (given correct), completion,
accuracy among completed, and realized generation length. No mediation
claim is identified by the parsed trace. Keep all outcomes. No
additional checkpoints, selective exclusions, or further runs guided
by the results.

A tokenizer-only preflight found the first denominator generator
(1.5 times the eligible total) cannot produce a count question with
both corrupted ratios integral. No inference ran. The multiplier was
changed to two before any model outputs were generated.
