# Evidence index — Time Capsule

This page documents the public, sanitized evidence for the Time Capsule HackerLab CTF task.

| File | Evidence |
|---|---|
| [`time-capsule-powershell-file-transfer.jpg`](./time-capsule-powershell-file-transfer.jpg) | Transfer of the challenge archive from Windows to the Ubuntu VM with `scp` over SSH |
| [`time-capsule-archive-extraction.jpg`](./time-capsule-archive-extraction.jpg) | Extraction of `task_time_capsule.zip` and discovery of the encrypted data file and helper executable |
| [`time-capsule-artifact-inspection.jpg`](./time-capsule-artifact-inspection.jpg) | Inventory of challenge artifacts, file-type identification, and SHA-256 integrity checks |
| [`time-capsule-age-container-extraction.jpg`](./time-capsule-age-container-extraction.jpg) | Extraction of the age-encrypted block into `capsule.age` and verification of the resulting file |
| [`time-capsule-tlock-plugin-help.jpg`](./time-capsule-tlock-plugin-help.jpg) | Verification of `age-plugin-tlock` availability and supported time-lock encryption options |
| [`time-capsule-task-completed.jpg`](./time-capsule-task-completed.jpg) | HackerLab confirmation that the task was solved successfully and the result was accepted; `+500 XP` awarded |

## Publication policy

The public repository intentionally excludes:

- The final CTF flag
- AES key material, IVs, or recovered seeds
- tlock identity files and private keys
- Original challenge archives and decrypted output
- Complete encrypted payloads when they are unnecessary for documentation
