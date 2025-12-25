# Домашнее задание к занятию «Защита хоста»  
**Выполнил:** Гридин Владимир

---

## Задание 1. Установка и настройка eCryptfs

### 1.1 Установка eCryptfs

```bash
sudo apt update
sudo apt install ecryptfs-utils
```

### 1.2 Добавление пользователя cryptouser

```bash
sudo adduser cryptouser
```

### 1.3 Шифрование домашнего каталога

```bash
sudo ecryptfs-migrate-home -u cryptouser
```

⚠️ Важно: После выполнения команды нужно перезайти под пользователем cryptouser, чтобы завершить процесс шифрования.

Скриншоты

Домашний каталог до шифрования

screenshots/cryptouser_before.png

Домашний каталог после шифрования

screenshots/cryptouser_after.png

## Задание 2. LUKS-шифрование раздела

### 2.1 Установка необходимых пакетов

```bash
sudo apt install cryptsetup
```

### 2.2 Создание раздела 100 Мб

Пример: создание файла-раздела и подключение через loop-устройство

```bash
dd if=/dev/zero of=/tmp/luks-volume bs=1M count=100
sudo losetup /dev/loop0 /tmp/luks-volume
```

### 2.3 Шифрование раздела LUKS

```bash
sudo cryptsetup luksFormat /dev/loop0
sudo cryptsetup open /dev/loop0 myencrypted
sudo mkfs.ext4 /dev/mapper/myencrypted
```

### 2.4 Монтирование и проверка

```bash
sudo mkdir /mnt/encrypted
sudo mount /dev/mapper/myencrypted /mnt/encrypted
df -h /mnt/encrypted
```

Скиншоты

Процесс создания и шифрования раздела

screenshots/luks_step1.png

Монтирование зашифрованного раздела

screenshots/luks_step2.png
