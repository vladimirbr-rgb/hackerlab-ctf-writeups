
# HackerLab CTF Write-ups

Учебные write-up'ы по заданиям HackerLab CTF. В репозитории собраны описание задач, использованные команды, подтверждающие скриншоты и выводы по прохождению.

> Все действия выполнялись исключительно в рамках учебной CTF-платформы и только с предоставленными артефактами.

## Environment

Лабораторная среда была подготовлена следующим образом:

- **Host OS:** Windows
- **Host terminal:** Windows PowerShell
- **Guest OS:** Ubuntu virtual machine
- **Guest shell:** Bash
- **Tools:** Linux CLI, `curl`, `age`, `age-plugin-tlock`, Cargo / Rust toolchain
- **Purpose:** практика администрирования Linux, анализа конфигураций, работы с криптографическими инструментами и CTF-артефактами.

## Completed tasks

| # | Task | Topic | Status |
|---|---|---|---|
| 1 | [Anonymizer — Decoding Client Records](./task-01/) | Python analysis, data decoding | Completed |
| 2 | [Time Capsule](./task-02-time-capsule/) | Time-lock encryption, age, drand, tlock | Completed |

## Repository structure

- [`task-01/`](./task-01/) — первое задание: анализ Python-обфускации и восстановление данных из учебных артефактов.
- [`task-02-time-capsule/`](./task-02-time-capsule/) — второе задание: расшифровка time-lock контейнера с помощью `age-plugin-tlock` и drand.
- В папках `commands/` сохранены использованные команды.
- В папках `screenshots/` размещены скриншоты процесса выполнения.

## Security note

Флаги, ключи, расшифрованные результаты и исходные файлы заданий не публикуются в репозитории. Это позволяет показать ход работы, не нарушая правила учебной CTF-платформы.
