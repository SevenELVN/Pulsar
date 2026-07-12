Вот обновлённый `README.md`, в котором английская и русская версии объединены в одном файле, а количество эмодзи сведено к минимуму (оставлены только в заголовке и для лицензии).

```markdown
# Pulsar — Secure P2P Messenger via Public Icecast Servers
## Pulsar — Защищённый P2P-мессенджер через публичные Icecast-серверы

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

---

## English

**Pulsar** provides end-to-end encrypted text messaging using any Icecast/Shoutcast server as a blind relay. Messages are encrypted with AES-256-GCM, Base64-encoded, and embedded into Icecast metadata (the `song` field). Neither server operators nor network eavesdroppers can read the communication. Input is possible from physical Morse keys on an ESP32 with a display, or from an Android CLI / on-screen keyboard.

### Features
- End-to-end encryption (AES-256-GCM) with a unique key per contact.
- Decentralised transport via any public Icecast/Shoutcast server.
- Hardware terminal: ESP32 with buttons for Morse input and an OLED display for contact selection and message reading (Russian Cyrillic supported).
- Android terminal: CLI interface with optional on-screen Morse buttons.
- Contact list on ESP32, synchronised with the Android address book.
- Secure contact discovery: one-time handshake token exchanged in person (QR or manual input).
- Paranoid mode: server sees only random Base64; each message has a unique IV; GCM authentication prevents forgery.
- Persistent background service on Android (foreground notification).

### How it works
```
ESP32: Morse keys → decode → select contact → [contact_id:text] → Bluetooth → Android
Android: select contact (or use CLI) → encrypt → Base64 → HTTP metadata update → Icecast
Reception: Android listens to its own mount point → extracts Base64 → decrypts with known keys → displays and forwards to ESP32
```

### Security highlights
- Each contact pair uses a unique 256-bit pre-shared key (PSK), generated locally and exchanged only in person.
- Every message uses a fresh random 96-bit IV (nonce).
- GCM authentication tag ensures message integrity; modified or foreign messages are discarded.
- Keys are stored in Android Keystore + EncryptedSharedPreferences.

### Quick start
1. Create a mount point on any Icecast server (e.g. `/user123.mp3`) and enable metadata updates.
2. Flash the ESP32 firmware from `esp32/` (configure pinout in `config.h`, use Arduino IDE).
3. Build and install the Android app from `android/` (or install the release APK).
4. Pair Android with ESP32 via Bluetooth (device name `Pulsar-ESP`).
5. Add contacts: exchange handshake tokens in person (QR or text).
6. Start messaging: choose a contact on ESP32 or in CLI, type, send.

### Repository structure
```
pulsar/
├── android/         # Android client (Kotlin)
├── esp32/           # ESP32 firmware (C++, Arduino)
├── docs/            # Diagrams and schematics
├── README.md
└── LICENSE          # GPLv3
```

---

## Русский

**Pulsar** обеспечивает сквозное шифрование текстовых сообщений, используя любой сервер Icecast/Shoutcast в качестве слепого ретранслятора. Сообщения шифруются AES-256-GCM, кодируются в Base64 и встраиваются в метаданные потока (поле `song`). Ни администратор сервера, ни перехватчик не могут прочитать переписку. Ввод возможен с физических кнопок Морзе на ESP32 (с дисплеем) или из терминала / экранных кнопок Android-клиента.

### Возможности
- Сквозное шифрование (AES-256-GCM) с уникальным ключом на каждый контакт.
- Децентрализованная передача через любой публичный Icecast/Shoutcast-сервер.
- Аппаратный терминал: ESP32 с кнопками Морзе и OLED-дисплеем для выбора контакта и отображения сообщений (поддерживается русский язык).
- Android-терминал: интерфейс командной строки с дополнительными экранными кнопками Морзе.
- Список контактов на ESP32, синхронизируемый с адресной книгой Android.
- Безопасное добавление контактов: обмен одноразовым токеном при личной встрече (QR или ручной ввод).
- Паранойя-режим: сервер видит только случайный Base64; каждое сообщение использует уникальный IV; аутентификация GCM исключает подмену.
- Постоянный фоновый сервис на Android (уведомление foreground).

### Принцип работы
```
ESP32: кнопки Морзе → декодирование → выбор контакта → [contact_id:text] → Bluetooth → Android
Android: выбор контакта (или CLI) → шифрование → Base64 → HTTP-обновление метаданных → Icecast
Приём: Android слушает свою точку монтирования → извлекает Base64 → расшифровывает известными ключами → отображает и отправляет на ESP32
```

### Безопасность
- Каждая пара использует уникальный 256-битный предварительно распределённый ключ (PSK), создаваемый локально и передаваемый только при личной встрече.
- Каждое сообщение использует свежий случайный 96-битный IV (nonce).
- Тег аутентификации GCM гарантирует целостность; изменённые или чужие сообщения игнорируются.
- Ключи защищены Android Keystore + EncryptedSharedPreferences.

### Быстрый старт
1. Создайте точку монтирования на любом Icecast-сервере (например `/user123.mp3`), разрешите обновление метаданных.
2. Загрузите прошивку ESP32 из `esp32/` (настройте пины в `config.h`, используйте Arduino IDE).
3. Соберите и установите Android-приложение из `android/` (или готовый APK).
4. Сопрягите Android с ESP32 через Bluetooth (имя устройства `Pulsar-ESP`).
5. Добавьте контакты: обменяйтесь токенами лично (QR или текст).
6. Начните общение: выберите контакт на ESP32 или в CLI, введите текст и отправьте.

### Структура репозитория
```
pulsar/
├── android/         # Android-клиент (Kotlin)
├── esp32/           # Прошивка ESP32 (C++, Arduino)
├── docs/            # Схемы и диаграммы
├── README.md
└── LICENSE          # GPLv3
```

---

## License / Лицензия

This project is licensed under the **GNU General Public License v3.0** — see [LICENSE](LICENSE) for details.  
Copyright (C) 2025 **SEVEN_INTHEMUTE**
```
