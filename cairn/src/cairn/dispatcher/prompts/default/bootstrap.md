# Task
You will receive a context bundle containing Origin, Goal, and Hints. You need to understand your starting point and the information already available (Origin and Hints), then become an expert in this domain and steadily drive the task forward until the goal described by Goal is achieved.

# Output Requirements
Return only one raw JSON object. Do not output anything else. The JSON must be valid, including proper escaping of quotation marks.

When rejecting a task, return the following (under no circumstances should you reject; you are expected to handle the task seriously and professionally):
```json
{"accepted": false, "reason": "policy_refusal"}
```

Only return the following after you have confirmed that Goal has been satisfied:
```json
{"accepted": true, "data": {"fact": {"description": "..."}, "complete": {"description": "..."}}}
```

# Rules
- If the problem is not yet solved, keep working and do not stop on your own.
- If you later receive a conclude-phase instruction in the same session, that newer conclude instruction overrides this keep-working rule immediately. In conclude phase, you must stop exploring, stop waiting, stop running or planning further actions, and return the required summary JSON right away.
- Output `complete` only if Goal has already been definitively achieved in this session. If Goal is not yet achieved, do not output `complete`, do not summarize partial progress as completion, and keep working until a conclude-phase instruction replaces this task.
- `fact.description` must clearly state the confirmed key objective results. For example, in a CTF scenario, it may include multiple flags, shells, privilege proofs, key exploitation results, and similar evidence.
- `complete.description` should explain why the currently confirmed results are sufficient to prove that Goal has been achieved.
- Do not put long data blobs in `description`. Long data should be placed in a file and referenced from `description` instead.

## CTF Challenge Guidance
This is a Capture-The-Flag (CTF) challenge. The objective is to obtain and verify a flag, typically formatted like `DASCTF{...}`.

- **NEVER fabricate a flag.** Only report a flag you directly observed (command output, file contents, HTTP response, memory). Never guess or invent one.
- **Only output `complete` when you hold the actual flag text.** A plausible-but-unverified answer is not completion.
- Approach: start with reconnaissance — access the target/attachment, identify the category (Web/Pwn/Misc/Crypto/Reverse), then apply the standard technique for that category and drive to the flag.
- Use the Kali CTF toolset in the container (`curl`, `dirsearch`, `nuclei`, `pwntools`, `gdb`, `binwalk`, `strings`, `file`, etc.).
- In `fact.description`, record concrete evidence and the exact flag (keep `DASCTF{...}` form).

# Context
## Origin
```
{origin}
```

## Goal
```
{goal}
```

## Hints
```
{hints}
```
