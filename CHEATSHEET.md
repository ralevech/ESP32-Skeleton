# ШПАРГАЛКА КОМАНД PLATFORMIO С ПОЯСНЕНИЯМИ

## ===== БАЗОВАЯ РАБОТА =====

**pio run** - Собрать (скомпилировать) проект. Создает прошивку .bin/.hex в папке .pio/build/

**pio run -e esp32dev** - Собрать проект для конкретной платы (esp32dev). Нужно если в platformio.ini прописано несколько сред

**pio run --target clean** - Очистить кэш сборки. Удаляет папку .pio/build/. Помогает при ошибках компиляции

**pio run --target clean && pio run** - Полная пересборка: сначала очистка, потом компиляция с нуля

## ===== ЗАГРУЗКА ПРОШИВКИ =====

**pio run --target upload** - Собрать и загрузить прошивку в микроконтроллер. Автоматически определяет COM-порт

**pio run -e esp32-c3-devkitm-1 --target upload** - Загрузить прошивку для конкретной платы (ESP32-C3)

**pio run --target upload --upload-port COM5** - Загрузить прошивку на указанный COM-порт. Нужно если подключено несколько плат

**pio run --target upload --upload-port COM5 --skip-build** - Загрузить уже готовую прошивку без пересборки. Экономит время

## ===== ФАЙЛОВАЯ СИСТЕМА =====

**pio run --target uploadfs** - Загрузить файловую систему (LittleFS/SPIFFS) из папки data/ в память МК

**pio run -e esp32dev --target uploadfs** - Загрузить файловую систему для конкретной платы

**pio run --target erasefs** - Стереть файловую систему. Очищает всю область SPIFFS/LittleFS

**pio run --target buildfs** - Создать образ файловой системы без загрузки в МК. Для проверки

## ===== МОНИТОР ПОРТА =====

**pio device monitor** - Открыть монитор COM-порта. Скорость берется из platformio.ini (monitor_speed)

**pio device monitor -b 115200** - Открыть монитор с явным указанием скорости. Нужно если скорость не совпадает с настройками

**pio device monitor -p COM5** - Открыть монитор на конкретном COM-порту

**pio device list** - Показать список всех доступных COM-портов с информацией о подключенных устройствах

## ===== БИБЛИОТЕКИ =====

**pio lib install "Adafruit NeoPixel"** - Установить библиотеку по имени из реестра PlatformIO

**pio lib install "Adafruit NeoPixel@1.7.0"** - Установить конкретную версию библиотеки

**pio lib install /path/to/library.zip** - Установить библиотеку из ZIP-архива (локально)

**pio lib install https://github.com/me-no-dev/ESPAsyncWebServer** - Установить библиотеку напрямую с GitHub

**pio lib update** - Обновить все установленные библиотеки до последних версий

**pio lib list** - Показать список всех установленных библиотек

**pio lib uninstall "Adafruit NeoPixel"** - Удалить библиотеку

## ===== ПЛАТФОРМЫ =====

**pio platform uninstall espressif32** - Удалить платформу ESP32. Очищает все файлы и тулы

**pio platform install espressif32** - Установить платформу ESP32 (последнюю версию)

**pio platform install espressif32@5.2.0** - Установить конкретную версию платформы

**pio platform update** - Обновить все установленные платформы до последних версий

**pio platform list** - Показать список установленных платформ с версиями

**pio platform search esp32** - Поиск платформ в реестре по ключевому слову

## ===== ОЧИСТКА И СБРОС =====

**pio run --target erase** - Полностью стереть flash-память. Удаляет все включая bootloader

**pio run --target erase && pio run --target upload** - Стереть flash и сразу залить новую прошивку

**pio run --target erase_eeprom** - Стереть только EEPROM (если поддерживается платой)

**pio device monitor --dtr** - Сбросить МК программно. Отправляет сигнал DTR через USB

## ===== ОБСЛУЖИВАНИЕ PIO =====

**pio upgrade** - Обновить ядро PlatformIO до последней версии

**pio system prune** - Очистить кэш и временные файлы PIO. Освобождает место

**pio system prune --force** - Принудительная очистка всех кэшей (включая библиотеки и платформы)

**pio system info** - Показать информацию о системе: пути, версии, установленные компоненты

**pio pkg install --tool platformio/tool-mklittlefs** - Установить утилиту для создания LittleFS (если нет в системе)

**pio pkg install --tool platformio/tool-mkspiffs** - Установить утилиту для создания SPIFFS

## ===== ESP32-CAM =====

**pio run --target upload --upload-speed 115200** - Загрузить прошивку на пониженной скорости. Стабильнее для ESP32-CAM

**pio run --target upload --upload-protocol esptool** - Использовать esptool для загрузки. Обходит проблемы с подключением

## ===== WEMOS D1 MINI (ESP8266) =====

**pio run --target upload --upload-speed 921600** - Загрузить с высокой скоростью (стандарт для NodeMCU/Wemos)

## ===== ARDUINO NANO / UNO =====

**pio run -e nano --board-option build.mcu=atmega328p** - Собрать с явным указанием типа процессора (ATmega328P)

**pio run --target burn-bootloader** - Записать bootloader. Требуется программатор (USBasp, ArduinoISP)

## ===== ОТЛАДКА =====

**pio run -v** - Собрать с подробным выводом (verbose). Показывает все флаги компиляции

**pio run --verbose** - Тоже самое, полный вывод всех процессов сборки

**pio run -t compiledb** - Сгенерировать файл compile_commands.json. Нужен для IDE (CLion, VS Code)

**pio check** - Статический анализ кода. Находит потенциальные ошибки и баги

**pio check --fix** - Автоматическое исправление найденных ошибок (если возможно)

## ===== ОКРУЖЕНИЯ =====

**pio run** - Собрать все среды из platformio.ini

**pio run -e esp32dev** - Собрать конкретную среду (esp32dev)

**pio run -e esp32-c3-devkitm-1 --target upload** - Загрузить прошивку для конкретной среды

**pio run -e wemos_d1_mini --target clean** - Очистить кэш для конкретной среды

**pio project config** - Показать конфигурацию текущего проекта (все среды, настройки)

## ===== ПОЛЕЗНЫЕ СЦЕНАРИИ =====

**pio run --target clean && pio run --target upload && pio device monitor** - Полный цикл: очистка → сборка → загрузка → монитор

**pio run --target uploadfs && pio run --target upload && pio device monitor** - Загрузить файловую систему + прошивку + открыть монитор

**pio upgrade && pio platform update && pio lib update** - Обновить всё: PIO, платформы, библиотеки

**pio system prune && pio run --target clean && pio run** - Полная очистка системы и пересборка проекта

**pio run --target upload --force** - Принудительная загрузка прошивки (игнорирует проверки)

**pio run --target size** - Показать использование памяти (RAM и Flash). Анализ размера прошивки

## ===== САМЫЕ ЧАСТЫЕ КОМАНДЫ =====

**pio run --target upload && pio device monitor** - Загрузить прошивку и сразу открыть монитор

**pio run --target uploadfs && pio run --target upload** - Загрузить файловую систему и прошивку

**pio run -e esp32dev** - Собрать проект для ESP32 DEVKIT

**pio run --target clean && pio run** - Очистить и пересобрать проект

**pio device list** - Посмотреть доступные COM-порты

---

**Сохраните эту шпаргалку в корне проекта как `PIO_CHEATSHEET.md`** — всегда будет под рукой! 🚀