# Anonymizer — Decoding Client Records

> Учебное задание HackerLab CTF по анализу обфусцированных данных и восстановлению содержимого файлов с помощью Python.

## Goal

Цель задания — проанализировать предоставленный архив с Python-скриптом и набором клиентских файлов, понять механизм преобразования данных и восстановить исходное содержимое, необходимое для завершения задания на HackerLab.

## Environment

Работа проводилась в изолированной лабораторной среде.

- **Host OS:** Windows
- **Host terminal:** Windows PowerShell
- **Guest OS:** Ubuntu virtual machine
- **Guest shell:** Bash
- **Tools:** `apt`, `unzip`, Python 3, Bash
- **Input artifacts:** `anonymizator.zip`, `anonymization.py`, `client1.txt`–`client4.txt`

Ubuntu VM была настроена и использовалась с Windows PC через PowerShell. Все действия выполнялись только с учебными CTF-материалами.

## Analysis

Архив задания содержал Python-скрипт обработки данных и несколько клиентских файлов. В ходе работы были выполнены следующие действия:

1. Проверена синхронизация времени и состояние Ubuntu environment.
2. Обновлён список пакетов и установлен `unzip`.
3. Распакован архив `anonymizator.zip`.
4. Определены доступные файлы: Python-скрипт и четыре клиентских артефакта.
5. Изучена логика преобразования данных.
6. Подготовлен и запущен Python-декодер `decode.py`.
7. Полученный результат был проверен и отправлен на платформу HackerLab.

## Safe reproduction steps

### Prepare the environment

```bash
sudo apt update
sudo apt install -y unzip
```

### Extract and inspect the artifact

```bash
unzip anonymizator.zip
find . -maxdepth 1 -type f -printf '%f\n' | sort
```

### Validate the decoder script

```bash
python3 -m py_compile decode.py
echo "Decoder script syntax check: OK"
```

> Команда расшифровки и её результат не публикуются, чтобы не раскрывать чувствительные учебные данные и итоговый флаг.

## Commands and evidence

- Использованные команды: [`commands/commands.md`](./commands/commands.md)
- Скриншоты выполнения: [`screenshots/`](./screenshots/)

## Result

Задание успешно завершено. Итоговый флаг был отправлен на платформу HackerLab.

В публичном репозитории не размещаются:

- итоговый флаг;
- исходные расшифрованные данные;
- персональные данные из учебных файлов;
- исходный архив задания;
- содержимое восстановленных клиентских записей.

## Key takeaway

Задание показало практический процесс анализа Python-скрипта и восстановления обработанных данных: от подготовки Linux-окружения и распаковки артефактов до проверки собственной логики декодирования.
