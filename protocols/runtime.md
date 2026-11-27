# Model and decoding settings

Gemma 4 31B IT and Qwen3-8B use their checkpoint chat templates with
thinking disabled, greedy BF16 generation (temperature 0), a 2,048-token
context, and a 16-token numeric readout for the two-task and ledger budget
runs. Gemma uses tensor parallelism 2. The Qwen run has one model replica.
The recorded versions are PyTorch 2.11.0, Transformers 5.12.1, tokenizers
0.22.2, NumPy 2.2.6 and vLLM 0.22.1rc1.dev166+gd0975a4b5.

The two-task run reads 64 and 192 review tokens. The budget run reads
192, 512 and 1,024. The earlier factorial uses Gemma 4 E4B IT and 31B IT,
64/320 review tokens and a 16-token staged readout. The single-generation
31B comparison uses 80/336 combined tokens. The archived natural-draft
experiment has 64/160 review caps and a 12-token readout.
