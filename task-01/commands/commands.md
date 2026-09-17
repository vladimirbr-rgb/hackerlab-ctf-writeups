# Commands — Network Configuration Analysis

В этом файле сохранены базовые команды, применявшиеся для анализа учебных артефактов в Ubuntu VM.

> Лабораторная среда была настроена на Windows PC через Windows PowerShell. Анализ выполнялся в Ubuntu virtual machine.

## Navigation and file inspection

```bash
pwd
ls -la
find . -maxdepth 2 -type f
```

## Inspect client configuration files

```bash
cat client1.txt
cat client2.txt
cat client3.txt
cat client4.txt
```

## Search for network-related parameters

```bash
grep -RniE 'vlan|ip|address|gateway|route|dns|network' .
```

## Network diagnostics

```bash
ip a
ip route
ip link
```

## Safe result handling

Результат был проверен и отправлен на учебной платформе HackerLab.

Флаг, пароли, токены, приватные адреса и иные чувствительные данные не публикуются.
