# Commands — Time Capsule

This file documents the safe, reproducible commands used during the Time Capsule HackerLab CTF task.

> The Ubuntu virtual machine was configured and accessed from a Windows PC through Windows PowerShell. The public repository does not include flags, identity files, keys, decrypted output, or original challenge artifacts.

## 1. Transfer the archive from Windows to Ubuntu

The challenge archive was transferred from Windows PowerShell to the Ubuntu VM with `scp`.

```powershell
scp -P 2222 "$env:USERPROFILE\Downloads\task_time_capsule.zip" `
  vladimir@localhost:/home/vladimir/ctf/hackerlab/time-capsule/
```

## 2. Connect to the Ubuntu VM

```powershell
ssh vladimir@localhost -p 2222
```

## 3. Open and inspect the task directory

```bash
cd ~/ctf/hackerlab/time-capsule
pwd
ls -lh
```

## 4. Extract the challenge archive

```bash
unzip task_time_capsule.zip
find . -maxdepth 2 -type f
```

## 5. Inspect the available artifacts

```bash
ls -lah
file mega_crypter very_important_data.crypt.enc
sha256sum mega_crypter very_important_data.crypt.enc
```

## 6. Extract the age container

```bash
sed -n '/-----BEGIN AGE ENCRYPTED FILE-----/,/-----END AGE ENCRYPTED FILE-----/p' \
  very_important_data.decrypted > capsule.age

ls -lh capsule.age
```

## 7. Verify the time-lock plugin

```bash
cargo --version
export PATH="$HOME/.cargo/bin:$PATH"
command -v age-plugin-tlock
age-plugin-tlock --help
```

## 8. Inspect the default drand chain

```bash
curl -s [https://api.drand.sh/info](https://api.drand.sh/info)
```

The default endpoint returned a drand chain hash that did not match the chain required by the CTF artifact.

## 9. Generate identity for the required chain

```bash
age-plugin-tlock --generate \
  --remote [https://api.drand.sh/52db9ba70e0cc0f6eaf7803dd07447a1f5477735fd3f661792ba94600c84e971](https://api.drand.sh/52db9ba70e0cc0f6eaf7803dd07447a1f5477735fd3f661792ba94600c84e971) \
  > tlock.key
```

## 10. Decrypt and validate the artifact

```bash
age --decrypt -i tlock.key -o final_capsule.txt capsule.age
file final_capsule.txt
wc -c final_capsule.txt
```

The final result was verified locally and submitted to HackerLab. The flag value is intentionally not included in this public documentation.

## Sensitive local files

The following files must not be committed to a public repository:

```text
task_time_capsule.zip
very_important_data.crypt.enc
very_important_data.decrypted
capsule.age
tlock.key
tlock-api-drand.key
final_capsule.txt
```
