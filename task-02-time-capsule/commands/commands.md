# Commands — Time Capsule

Этот файл содержит команды, применённые для выполнения учебного задания HackerLab CTF в Ubuntu VM.

> Ubuntu virtual machine была настроена и использовалась с Windows PC через Windows PowerShell. В публичный репозиторий не добавляются ключи, расшифрованные файлы и итоговый флаг.

## 1. Verify the environment

```bash
cargo --version
export PATH="$HOME/.cargo/bin:$PATH"
command -v age-plugin-tlock
age-plugin-tlock --help
```

## 2. Check the default drand chain

```bash
curl -s [https://api.drand.sh/info](https://api.drand.sh/info)
```

The default endpoint returned a chain hash that did not match the chain required by the CTF artifact.

## 3. Generate tlock identity for the required chain

```bash
age-plugin-tlock --generate \
  --remote [https://api.drand.sh/52db9ba70e0cc0f6eaf7803dd07447a1f5477735fd3f661792ba94600c84e971](https://api.drand.sh/52db9ba70e0cc0f6eaf7803dd07447a1f5477735fd3f661792ba94600c84e971) \
  > tlock.key
```

## 4. Decrypt the artifact

```bash
age --decrypt -i tlock.key -o final_capsule.txt capsule.age
```

## 5. Validate the output

```bash
file final_capsule.txt
wc -c final_capsule.txt
grep -a -nE 'CODEBY\{[^}]+\}' final_capsule.txt
```

## Sensitive local files

The following local files must not be committed to a public repository:

```text
capsule.age
tlock.key
tlock-api-drand.key
final_capsule.txt
```
