# 🚀 Pulsar
### Secure P2P Messenger via Public Icecast Servers
### Защищённый P2P-мессенджер через публичные Icecast-серверы

<p align="center">

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
![Platform](https://img.shields.io/badge/Platform-Android%20%7C%20ESP32-success)
![Encryption](https://img.shields.io/badge/Encryption-AES--256--GCM-red)
![Transport](https://img.shields.io/badge/Transport-Icecast%20%2F%20Shoutcast-orange)

</p>

---

# 🇬🇧 English

## Overview

**Pulsar** is an end-to-end encrypted messenger that uses any public **Icecast/Shoutcast** server as a blind relay.

Instead of sending ordinary chat packets, encrypted messages are embedded into the stream metadata (`song` field). Server operators only see random Base64 strings and cannot decrypt or modify the communication.

Messages can be entered using:

- 📱 Android CLI
- ⌨️ Android on-screen Morse keyboard
- 📟 ESP32 hardware terminal with physical Morse keys and OLED display

---

## ✨ Features

- 🔐 AES-256-GCM end-to-end encryption
- 🔑 Unique 256-bit key for every contact
- 🌐 Works through any public Icecast/Shoutcast server
- 📟 ESP32 hardware messenger
- 📱 Android terminal (CLI + optional Morse buttons)
- 📚 Contact list synchronized with Android
- 🤝 Secure in-person contact exchange (QR or manual token)
- 🛡️ Fresh IV for every message
- ✅ GCM authentication prevents forgery
- 🔔 Persistent Android background service

---

## 🏗 Architecture

```text
ESP32
  │
  │ Morse buttons
  ▼
Decode Morse
  │
Select Contact
  │
[contact_id:text]
  │
Bluetooth
  ▼
Android
  │
AES-256-GCM
  │
Base64
  │
HTTP Metadata Update
  ▼
Icecast/Shoutcast Server
  │
(song metadata)
  ▼
Android Receiver
  │
Decrypt
  ▼
ESP32 Display
```

---

## 🔒 Security

Every contact pair has its own locally generated **256-bit PSK**.

For every message:

- random 96-bit IV (nonce)
- AES-256-GCM encryption
- authentication tag verification

Modified, forged or foreign packets are discarded automatically.

Encryption keys are stored securely using:

- Android Keystore
- EncryptedSharedPreferences

---

## 🚀 Quick Start

### 1. Prepare Icecast

Create a mount point such as:

```
/user123.mp3
```

Enable metadata updates.

### 2. Flash ESP32

Firmware:

```
esp32/
```

Configure:

```
config.h
```

Upload using Arduino IDE.

### 3. Install Android App

Build:

```
android/
```

or install the Release APK.

### 4. Pair Devices

Bluetooth device:

```
Pulsar-ESP
```

### 5. Exchange Contacts

Exchange one-time handshake tokens:

- QR code
- Manual text

### 6. Start Messaging

Choose a contact, type your message and send.

---

## 📁 Repository Structure

```text
pulsar/
├── android/          # Android client (Kotlin)
├── esp32/            # ESP32 firmware (Arduino/C++)
├── docs/             # Schematics & diagrams
├── README.md
└── LICENSE
```

---

# 🇷🇺 Русский

## Описание

**Pulsar** — это мессенджер со сквозным шифрованием, использующий любой публичный сервер **Icecast/Shoutcast** как слепой ретранслятор.

Сообщения шифруются алгоритмом **AES-256-GCM**, кодируются в Base64 и помещаются в метаданные потока (`song`).

Администратор сервера и любой перехватчик видят только случайные данные и не могут прочитать переписку.

Ввод возможен:

- 📱 из Android CLI
- ⌨️ экранными кнопками Морзе
- 📟 аппаратной клавиатурой Морзе на ESP32

---

## ✨ Возможности

- 🔐 Сквозное шифрование AES-256-GCM
- 🔑 Отдельный ключ для каждого контакта
- 🌐 Передача через любой публичный Icecast/Shoutcast
- 📟 Аппаратный терминал ESP32
- 📱 Android-клиент (CLI + кнопки Морзе)
- 📚 Синхронизация списка контактов
- 🤝 Добавление контактов через QR или одноразовый токен
- 🛡️ Новый IV для каждого сообщения
- ✅ Проверка целостности GCM
- 🔔 Постоянный foreground-сервис Android

---

## 🏗 Схема работы

```text
ESP32
  │
Кнопки Морзе
  ▼
Декодирование
  │
Выбор контакта
  │
[contact_id:text]
  │
Bluetooth
  ▼
Android
  │
AES-256-GCM
  │
Base64
  │
HTTP обновление metadata
  ▼
Icecast/Shoutcast
  │
(song)
  ▼
Android
  │
Расшифровка
  ▼
ESP32
```

---

## 🔒 Безопасность

Для каждой пары пользователей создаётся собственный **256-битный PSK**, который передаётся только лично.

Каждое сообщение использует:

- случайный IV (96 бит)
- AES-256-GCM
- проверку аутентификационного тега

Изменённые или поддельные сообщения автоматически отбрасываются.

Ключи защищены средствами Android:

- Android Keystore
- EncryptedSharedPreferences

---

## 🚀 Быстрый старт

### 1. Настройте Icecast

Создайте точку монтирования:

```
/user123.mp3
```

Разрешите обновление metadata.

### 2. Прошейте ESP32

Прошивка:

```
esp32/
```

Настройте:

```
config.h
```

Загрузите через Arduino IDE.

### 3. Установите Android

Соберите приложение из:

```
android/
```

или установите готовый APK.

### 4. Сопрягите устройства

Bluetooth:

```
Pulsar-ESP
```

### 5. Добавьте контакты

Обменяйтесь одноразовыми токенами:

- QR-код
- текстовый код

### 6. Общайтесь

Выберите контакт, введите сообщение и отправьте.

---

## 📁 Структура проекта

```text
pulsar/
├── android/          # Android-клиент (Kotlin)
├── esp32/            # Прошивка ESP32 (Arduino/C++)
├── docs/             # Схемы и диаграммы
├── README.md
└── LICENSE
```

---

# 📜 License / Лицензия

Licensed under the **GNU General Public License v3.0 (GPL-3.0)**.

See **LICENSE** for details.

---

<p align="center">

Made with ❤️ for secure decentralized communication.

**Copyright © 2026 SEVEN_INTHEMUTE**

</p>
