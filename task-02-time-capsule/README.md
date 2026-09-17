# Time Capsule

> Учебное криптографическое задание HackerLab CTF: расшифровка time-lock контейнера `age` с использованием `age-plugin-tlock` и сети drand.

## Goal

Цель задания — получить содержимое защищённого файла `capsule.age`, связанного с конкретным раундом сети drand.

Для успешного выполнения требовалось:

1. Проверить доступность `age-plugin-tlock`.
2. Определить drand chain, использованную при шифровании.
3. Создать корректный tlock identity для нужной цепочки.
4. Расшифровать контейнер `capsule.age`.
5. Проверить полученный результат и отправить флаг на платформу HackerLab.

## Environment

Работа выполнялась в изолированной учебной среде.

- **Host OS:** Windows
- **Host terminal:** Windows PowerShell
- **Guest OS:** Ubuntu virtual machine
- **Guest shell:** Bash
- **Tools:** `curl`, `age`, `age-plugin-tlock`, Cargo / Rust toolchain
- **Randomness network:** [drand](https://drand.love/)

Ubuntu VM была настроена и использовалась с Windows PC через PowerShell. Все действия выполнялись только с учебными CTF-артефактами.

## Technical analysis

Зашифрованный файл использовал recipient типа `tlock`. Такой механизм связывает расшифровку с конкретной сетью drand и опубликованным раундом случайности.

Проверка общего endpoint:

```text
[https://api.drand.sh/info](https://api.drand.sh/info)
```

показала default drand chain с hash:

```text
8990e7a9aaed2ffed73dbd7092123d6f289930540d7651336225dc172e51b2ce
```

Этот идентификатор не совпадал с цепочкой, указанной в параметрах CTF-контейнера. Для расшифровки требовалась другая drand chain:

```text
52db9ba70e0cc0f6eaf7803dd07447a1f5477735fd3f661792ba94600c84e971
```

После генерации identity для chain-specific endpoint контейнер был успешно расшифрован.

## Solution path

### 1. Check the tools

```bash
cargo --version
export PATH="$HOME/.cargo/bin:$PATH"
command -v age-plugin-tlock
age-plugin-tlock --help
```

### 2. Inspect the default drand endpoint

```bash
curl -s [https://api.drand.sh/info](https://api.drand.sh/info)
```

### 3. Generate an identity for the required chain

```bash
age-plugin-tlock --generate \
  --remote [https://api.drand.sh/52db9ba70e0cc0f6eaf7803dd07447a1f5477735fd3f661792ba94600c84e971](https://api.drand.sh/52db9ba70e0cc0f6eaf7803dd07447a1f5477735fd3f661792ba94600c84e971) \
  > tlock.key
```

### 4. Decrypt the challenge artifact

```bash
age --decrypt -i tlock.key -o final_capsule.txt capsule.age
```

### 5. Validate the output

```bash
file final_capsule.txt
wc -c final_capsule.txt
grep -a -nE 'CODEBY\{[^}]+\}' final_capsule.txt
```

## Commands and evidence

- Полный набор команд: [`commands/commands.md`](./commands/commands.md)
- Скриншоты выполнения: [`screenshots/`](./screenshots/)

## Result

Задание успешно завершено, а итоговый флаг был проверен и отправлен на HackerLab.

В целях соблюдения правил CTF в репозитории не публикуются флаг, расшифрованный результат, ключи/identity и исходный контейнер задания.

## Key takeaway

Для time-lock шифрования недостаточно обратиться к произвольному endpoint drand. Необходимо использовать endpoint той же drand chain, которая указана в recipient зашифрованного контейнера.
