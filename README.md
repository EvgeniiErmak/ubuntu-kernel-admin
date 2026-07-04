# Обновление ядра системы

## Цель

Обновить ядро Ubuntu до последней стабильной версии из mainline-репозитория.

## Ход выполнения

Сначала проверил текущую версию ядра:

```bash
uname -r
```

Результат:

```text
6.8.0-49-generic
```

Создал рабочую директорию и скачал пакеты ядра версии 7.1.0:

```bash
mkdir kernel && cd kernel

wget https://kernel.ubuntu.com/mainline/v7.1/amd64/linux-headers-7.1.0-070100-generic_7.1.0-070100.202606141628_amd64.deb
wget https://kernel.ubuntu.com/mainline/v7.1/amd64/linux-headers-7.1.0-070100_7.1.0-070100.202606141628_all.deb
wget https://kernel.ubuntu.com/mainline/v7.1/amd64/linux-image-unsigned-7.1.0-070100-generic_7.1.0-070100.202606141628_amd64.deb
wget https://kernel.ubuntu.com/mainline/v7.1/amd64/linux-modules-7.1.0-070100-generic_7.1.0-070100.202606141628_amd64.deb
```

Установил скачанные пакеты:

```bash
sudo dpkg -i *.deb
```

Проверил, что новое ядро установлено:

```bash
ls -al /boot | grep vmlinuz
```

Результат:

```text
lrwxrwxrwx 1 root root 29 Jun 14 17:33 vmlinuz -> vmlinuz-7.1.0-070100-generic
-rw------- 1 root root 17825792 Jun 14 17:31 vmlinuz-7.1.0-070100-generic
-rw------- 1 root root 14956936 Nov  1 11:41 vmlinuz-6.8.0-49-generic
lrwxrwxrwx 1 root root 24 Jun 14 17:33 vmlinuz.old -> vmlinuz-6.8.0-49-generic
```

Обновил конфигурацию загрузчика и назначил новое ядро по умолчанию:

```bash
sudo update-grub
sudo grub-set-default 0
```

Перезагрузил систему:

```bash
sudo reboot
```

После перезагрузки проверил установленную версию ядра:

```bash
uname -r
```

Результат:

```text
7.1.0-070100-generic
```

## Итог

Задание выполнено. Ядро Ubuntu успешно обновлено с версии `6.8.0-49-generic` до `7.1.0-070100-generic`.
