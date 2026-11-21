# 🤖 GigaChat CLI

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![GigaChat](https://img.shields.io/badge/GigaChat-Pro-green.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

**Мощный консольный инструмент для взаимодействия с моделью GigaChat через командную строку**

[Возможности](#-функционал) • [Установка](#-установка) • [Примеры](#-примеры-использования) • [Алиасы](#-как-добавить-алиас)

</div>

---

## 📋 Описание

**GigaChat CLI** — это удобный инструмент командной строки для работы с моделью **GigaChat** от Сбера. Позволяет отправлять текст, код, логи или коммиты на анализ, объяснение, перевод или суммирование прямо из терминала.

### 🎯 Основные преимущества

- ⚡ **Быстрый доступ** - работа с AI прямо из командной строки
- 🔄 **Гибкость** - поддержка stdin и аргументов командной строки
- 🎨 **Удобные флаги** - предустановленные команды для типовых задач
- 🛠 **Кастомизация** - возможность задать собственный префикс запроса
- 📦 **Простота** - минимальная настройка, максимум функциональности

---

## 🛠 Функционал

### Основные возможности:

- ✅ Отправка сообщений в GigaChat
- ✅ Чтение ввода из stdin (например: `echo "текст" | python main.py`)
- ✅ Чтение из аргументов командной строки
- ✅ Поддержка пользовательских и стандартных флагов
- ✅ Гибкая настройка через переменные окружения

### 📌 Доступные флаги:

| Флаг | Описание |
|------|----------|
| `--help` | Вывести список доступных флагов |
| `--check-code` | Проверка и анализ кода |
| `--review-commit` | Ревью коммита Git |
| `--explain` | Объяснение концепций и терминов |
| `--check-log` | Анализ логов и объяснение ошибок |
| `--summarize` | Суммирование текста |
| `--translate` | Перевод на русский язык |
| `--prompt "..."` | Пользовательский префикс запроса |

---

## 📦 Установка

### Шаг 1: Установка зависимостей

```bash
pip install gigachat python-dotenv
```

### Шаг 2: Настройка переменных окружения

Создайте файл `.env` в корне проекта со следующим содержимым:

```env
GIGACHAT_CREDENTIALS=ваш_токен
GIGACHAT_MODEL=GigaChat-Pro
VERIFY_SSL_CERTS=false
```

> 💡 **Где получить токен?**
> Токен можно получить на [официальном сайте GigaChat](https://developers.sber.ru/gigachat)

---

## 🚀 Примеры использования

### Базовое использование

```bash
python main.py "Объясни на русском Что такое ООП?"
```

### Работа с stdin

```bash
echo "Как работает Python?" | python main.py
```

```bash
cat file.txt | python main.py
```

### Использование флагов

#### Проверка кода

```bash
echo "def hello():\n    print('Hello')" | python main.py --check-code
```

```bash
cat index.php | python main.py --check-code
```

#### Ревью коммита

```bash
git show HEAD | python main.py --review-commit
```

#### Объяснение концепций

```bash
echo "Что такое рекурсия?" | python main.py --explain
```

#### Анализ логов

```bash
tail laravel.log | python main.py --check-log
```

#### Суммирование текста

```bash
cat long_article.txt | python main.py --summarize
```

#### Перевод

```bash
echo "Hello, world!" | python main.py --translate
```

### Пользовательский префикс

```bash
tail laravel.log | python main.py --prompt "Объясни на русском"
```

```bash
cat code.py | python main.py --prompt "Найди ошибки в коде"
```

---

## 🐍 Как добавить алиас для удобного запуска

Создайте алиас, чтобы не писать каждый раз `python main.py`, а использовать короткое имя — например, `giga`.

### Для Bash (Linux/macOS)

Добавьте в файл `~/.bashrc` или `~/.zshrc`:

```bash
alias giga='python /путь/к/проекту/main.py'
```

Примените изменения:

```bash
source ~/.bashrc  # или source ~/.zshrc
```

Теперь вы можете использовать:

```bash
echo "Как работает рекурсия?" | giga --explain
```

```bash
cat code.py | giga --check-code
```

### Для Windows (PowerShell)

Откройте PowerShell и выполните:

```powershell
Set-Alias -Name giga -Value "C:\путь\к\проекту\main.py"
```

Или добавьте это в ваш `profile.ps1`:

```powershell
if (!(Get-Alias -Name giga -ErrorAction SilentlyContinue)) {
    Set-Alias -Name giga -Value "C:\путь\к\проекту\main.py"
}
```

Чтобы найти путь к `profile.ps1`:

```powershell
$PROFILE
```

---

## 📊 Сравнение использования

### Без алиаса:
```bash
python /long/path/to/project/main.py --check-code < file.py
```

### С алиасом:
```bash
giga --check-code < file.py
```

---

## 🔧 Расширенные примеры

### Комбинирование с другими инструментами

```bash
# Анализ последних 50 строк лога
tail -n 50 app.log | giga --check-log

# Ревью последнего коммита
git show HEAD | giga --review-commit

# Перевод файла
cat english.txt | giga --translate > russian.txt

# Объяснение сложного кода
cat complex_algorithm.py | giga --explain
```

### Использование в скриптах

```bash
#!/bin/bash
# Скрипт для автоматического ревью коммитов

COMMIT_MSG=$(git log -1 --pretty=%B)
echo "$COMMIT_MSG" | giga --review-commit
```

---

## 🧩 Возможные улучшения

- [ ] Поддержка нескольких флагов одновременно
- [ ] Автоматическое форматирование кода
- [ ] Логирование запросов и ответов
- [ ] Кэширование результатов
- [ ] Поддержка файлов конфигурации
- [ ] Цветной вывод в терминале
- [ ] Поддержка других моделей GigaChat

---

## ✅ Требования

- **Python 3.8+**
- **gigachat** - [PyPI](https://pypi.org/project/gigachat/)
- **python-dotenv** - [PyPI](https://pypi.org/project/python-dotenv/)

---

## 🐛 Решение проблем

### Ошибка: "Please provide a message"
- **Причина:** Не указано сообщение ни в аргументах, ни в stdin
- **Решение:** Укажите сообщение как аргумент или передайте через stdin

### Ошибка: "GIGACHAT_CREDENTIALS not found"
- **Причина:** Не настроен файл `.env` или не указан токен
- **Решение:** Создайте файл `.env` с правильными переменными

### Ошибка подключения
- **Причина:** Проблемы с сетью или неверный токен
- **Решение:** Проверьте интернет-соединение и валидность токена

---

---

Автор: legenda  
Telegram: [@LEGENDA_SD](https://t.me/LEGENDA_SD)
