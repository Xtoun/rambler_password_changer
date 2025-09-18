# rambler_password_changer



Python script for automatic rambler password change with proxy support and 2captcha integration


- [Запуск под Windows](#запуск-под-windows)
- [Data / config](#Data-/-config)
- [Настройка 2Captcha](#настройка-2captcha)
- [Настройка прокси](#настройка-прокси)

## Запуск под Windows
- Установите [Python 3.11](https://www.python.org/downloads/windows/). Не забудьте поставить галочку напротив "Add Python to PATH".
- Установите [git](https://git-scm.com/download/win). Это позволит с легкостью получать обновления скрипта командой `git pull`
- Откройте консоль в удобном месте...
  - Склонируйте (или [скачайте](https://github.com/Xtoun/rambler_password_changer/archive/refs/heads/main.zip)) этот репозиторий:
    ```bash
    git clone https://github.com/Xtoun/rambler_password_changer.git
    ```
  - Перейдите в папку проекта:
    ```bash
    cd rambler_password_changer
    ```
  - Установите требуемые зависимости следующей командой или запуском файла `INSTALL.bat`:
    ```bash
    pip install -r requirements.txt
    playwright install
    ```
  - Запустите скрипт следующей командой или запуском файла `START.bat`:
    ```bash
    python main.py
    ```

## Data / config

- После запуска START.bat появятся файлы `old_password.txt` и `proxy.txt`
- В `old_password.txt` вставьте почты в формате:
    ```bash
    login:password
    login:password
    login:password
    ...
    ```
- В `proxy.txt` вставьте прокси в формате (опционально):
    ```bash
    http://user:pass@proxy1.com:8080
    http://proxy2.com:3128
    http://user:pass@192.168.1.1:8080
    ```
- В файл `config.py` вставьте API-key от 2captcha.com:
    ```python
    CAPTCHA_KEY = 'ваш_api_ключ_от_2captcha' # "2captcha.com"
    ```

## Настройка 2Captcha

1. Зарегистрируйтесь на [2captcha.com](https://2captcha.com)
2. Получите API-ключ в личном кабинете
3. Пополните баланс аккаунта
4. Вставьте API-ключ в файл `data/config.py`

### Поддерживаемые типы капч
- hCaptcha (основной тип, используемый в проекте)
- reCAPTCHA v2/v3
- FunCaptcha
- GeeTest

## Настройка прокси

Проект поддерживает использование прокси для повышения анонимности и обхода блокировок.

### Поддерживаемые типы прокси

1. **HTTP прокси**:
   ```
   http://username:password@host:port
   http://host:port
   ```

### Настройка прокси

1. **Создайте файл `data/proxy.txt`** (если его нет, он создастся автоматически при первом запуске)

2. **Добавьте прокси в файл** - каждая строка должна содержать один прокси:
   ```
   http://user1:pass1@proxy1.com:8080
   http://proxy2.com:3128
   http://user3:pass3@proxy3.com:8080
   http://user4:pass4@192.168.1.1:8080
   ```

3. **Важно**: Прокси выбираются **случайным образом** из доступных
   - Можно иметь любое количество прокси (от 1 и больше)
   - Каждый аккаунт получит случайный прокси из списка
   - Если прокси мало - будут использоваться повторно случайно
   - Если прокси много - будут выбираться случайные из всех доступных

4. **При запуске** выберите "Да" на вопрос "Использовать прокси?"