# Commands — Anonymizer

This file documents the safe, reproducible commands used during the Anonymizer HackerLab CTF task.

> The lab environment was prepared on a Windows PC through Windows PowerShell. The analysis was performed in an Ubuntu virtual machine using Bash and Python 3.

## 1. Verify time synchronization and update packages

```bash
sudo systemctl status chrony
sudo chronyc -a makestep
date
timedatectl
sudo apt update
```

## 2. Install the archive extraction utility

```bash
sudo apt install -y unzip
```

## 3. Open the task directory

```bash
cd ~/ctf/hackerlab/anonymizer
pwd
```

## 4. Inspect the challenge archive

```bash
unzip -l anonymizator.zip
```

## 5. Inventory available files

```bash
find . -maxdepth 1 -type f -printf '%f\n' | sort
```

Expected artifact names:

```text
anonymization.py
anonymizator.zip
client1.txt
client2.txt
client3.txt
client4.txt
decode.py
```

## 6. Validate the decoder

```bash
python3 -m py_compile decode.py
echo "Decoder script syntax check: OK"
```

## Result handling

The task was completed successfully and the result was accepted by HackerLab.

The public repository intentionally does not include:

- The final CTF flag
- Decoded client records
- Personal data from challenge artifacts
- The original archive
- Credentials, private keys, tokens, or passwords
