# PPitStop Planner

**Developers: [oniqq1](https://github.com/oniqq1)**

PPitStop Planner is a Windows companion application for **Le Mans Ultimate**. It combines live telemetry uploading, pit-stop strategy planning, an in-game overlay, local consumption history, and remote access through the PPitStop Planner website.

Releases and downloads: [PPitStopPlanner-releases](https://github.com/oniqq1/PPitStopPlanner-releases/releases)

## Features

### LMU Control Center

The desktop launcher starts the live uploader automatically and provides one place to manage the application:

- start and stop the pit-plan overlay;
- configure the shared Session code;
- view and copy the Personal uploader code;
- enable automatic startup with Windows;
- minimize the application to the system tray;
- check for and install updates from GitHub Releases.

If no Session code is provided, the application restores the previously saved code or creates a new `AUTO...` code.

### Live telemetry uploader

The uploader reads data from LMU REST endpoints and shared memory, then sends the active session telemetry to the planner server.

It provides:

- current driver, car, track, class, position, and lap;
- fuel and Virtual Energy state;
- tyre condition and wear information;
- car damage and pit status;
- lap times and race progress;
- telemetry for the manager view;
- automatic detection of an active LMU session.

The launcher displays three uploader states:

- **Script started**;
- **Waiting for game**;
- **Script working**.

### Clean-lap consumption measurement

The uploader measures fuel and Virtual Energy consumption from clean completed laps.

- The first lap transition after startup is skipped to avoid recording a partial lap.
- Pit laps and unsuitable laps are excluded.
- A median consumption value becomes available after at least three clean laps.
- Up to 20 personal samples are retained for each car and track combination.
- Previous personal history is used until enough new clean laps are collected.

Personal measurements are stored locally in:

```text
Documents\PPitStopPlanner\personal_consumption.json
```

### Pit-stop strategy planner

The planner supports races configured by lap count or duration and calculates stints using:

- fuel consumption;
- Virtual Energy consumption;
- tyre wear;
- Hypercar battery limits;
- fuel-tank capacity;
- minimum tyre condition.

Available planning tools include:

- automatic pit-stop calculation;
- manual pit-stop markers;
- tyre-change selection for every stop;
- recommended starting fuel and pit-stop refuelling;
- strategy saving and loading;
- automatic strategy names based on the driver, track, and layout.

### Pit-plan overlay

The PySide6 overlay displays the current strategy over the game.

It can show:

- starting fuel and Virtual Energy before the race;
- the next planned pit lap;
- required pit-stop fuel and VE;
- fuel-to-VE ratio;
- current car and plan information.

Fuel and VE consumption can be adjusted directly from the overlay. The strategy is recalculated immediately, and the values are saved to the local user configuration.

Press `F8` to enter preview mode, move the overlay, and save its position.

### Local car and track settings

User-specific car and track data is stored in:

```text
Documents\PPitStopPlanner\trackDefaults.json
```

The original reference data is stored separately in:

```text
Documents\PPitStopPlanner\trackDefaults.base.json
```

The base file remains unchanged. Manual fuel and VE values from the website or overlay are written only to `trackDefaults.json`.

Local values have priority in future calculations:

1. manual local values;
2. personal clean-lap history;
3. car and track presets;
4. general track defaults.

The live uploader transfers only values that differ from the base configuration.

### Website synchronization

The website and desktop application communicate through the live uploader.

- Changes made on the website are queued on the server.
- The uploader receives the command in its next telemetry response.
- The corresponding local `trackDefaults.json` entry is updated.
- The uploader sends the local difference back to the website.
- The base configuration is never modified.

The connection is identified by the combination of the Session code and Personal uploader code.

### Manager mode and race results

The manager interface provides live information for cars in a shared session, including:

- overall and class positions;
- lap and timing information;
- fuel and VE estimates;
- tyre condition;
- pit stops and pit status;
- damage information;
- individual strategy details.

Completed race information can be stored in the race-results archive.

### Best laps and leaderboard

Registered users can bind their live session and publish verified LMU lap times. The application supports:

- best laps by car class and track;
- practice, qualifying, and race session types;
- driver profiles;
- weather information;
- reference pace levels;
- a public leaderboard.

## Local data

Application settings and identifiers are stored in:

```text
%LOCALAPPDATA%\PPitStopPlanner\
```

Long-term user data is stored in:

```text
Documents\PPitStopPlanner\
```

User data is not overwritten by application updates.

## Requirements

- Windows 10 or Windows 11;
- Le Mans Ultimate;
- LMU shared memory and local REST API access;
- internet connection for website synchronization and updates.

## Updates

The application checks for new versions through GitHub Releases. Updates replace program files only and preserve local settings, personal consumption history, and track data.


/n
/n
---
/n
/n





# PPitStop Planner — українська версія

**Розробник: [oniqq1](https://github.com/oniqq1)**

PPitStop Planner — це Windows-застосунок-компаньйон для **Le Mans Ultimate**. Він поєднує передачу live-телеметрії, планування піт-стопів, ігровий оверлей, локальну історію витрати ресурсів та віддалений доступ через сайт PPitStop Planner.

Релізи та завантаження: [PPitStopPlanner-releases](https://github.com/oniqq1/PPitStopPlanner-releases/releases)

## Функціонал

### LMU Control Center

Лаунчер автоматично запускає live uploader та дозволяє керувати застосунком з одного вікна:

- запускати й зупиняти оверлей піт-плану;
- налаштовувати спільний Session code;
- переглядати та копіювати Personal uploader code;
- вмикати автоматичний запуск разом із Windows;
- згортати застосунок у системний трей;
- перевіряти та встановлювати оновлення з GitHub Releases.

Якщо Session code не вказаний, застосунок використовує збережений код або створює новий код формату `AUTO...`.

### Передача live-телеметрії

Uploader читає дані з LMU REST API та shared memory, після чого передає телеметрію активної сесії на сервер планувальника.

Передаються:

- пілот, автомобіль, траса, клас, позиція та коло;
- запас пального та Virtual Energy;
- стан і знос шин;
- пошкодження автомобіля та стан піт-стопу;
- час кіл і перебіг гонки;
- дані для менеджерського режиму;
- статус активної LMU-сесії.

Лаунчер показує три стани uploader:

- **Скрипт запущено**;
- **Скрипт очікує гру**;
- **Скрипт працює**.

### Вимірювання витрати на чистих колах

Uploader вимірює витрату пального та Virtual Energy за завершеними чистими колами.

- Перше перетинання лінії після запуску пропускається, щоб не записати неповне коло.
- Піт-коли та непридатні кола не потрапляють у вибірку.
- Медіанне значення стає доступним після щонайменше трьох чистих кіл.
- Для кожної комбінації автомобіля і траси зберігається до 20 особистих вимірювань.
- Попередня особиста історія використовується, доки не накопичено достатньо нових кіл.

Особисті вимірювання зберігаються локально:

```text
Документи\PPitStopPlanner\personal_consumption.json
```

### Планувальник піт-стопів

Планувальник підтримує гонки за кількістю кіл або тривалістю та розраховує стінти з урахуванням:

- витрати пального;
- витрати Virtual Energy;
- зносу шин;
- обмежень батареї Hypercar;
- місткості паливного бака;
- мінімально допустимого стану шин.

Доступні можливості:

- автоматичний розрахунок піт-стопів;
- ручне переміщення маркерів зупинок;
- вибір заміни шин на кожному піт-стопі;
- рекомендації щодо стартового пального та дозаправлення;
- збереження і завантаження стратегій;
- автоматичні назви стратегій за пілотом, трасою та конфігурацією.

### Оверлей піт-плану

Оверлей на PySide6 показує поточну стратегію поверх гри.

Він може показувати:

- стартовий запас пального та VE перед гонкою;
- коло наступного запланованого піт-стопу;
- потрібну кількість пального та VE;
- співвідношення пального до VE;
- поточний автомобіль та інформацію про план.

Витрату пального та VE можна змінювати безпосередньо в оверлеї. Стратегія одразу перераховується, а значення зберігаються в локальній конфігурації користувача.

Натисніть `F8`, щоб увімкнути режим попереднього перегляду, перемістити оверлей і зберегти його позицію.

### Локальні налаштування машин і трас

Особисті дані автомобілів і трас зберігаються у файлі:

```text
Документи\PPitStopPlanner\trackDefaults.json
```

Початкові еталонні дані зберігаються окремо:

```text
Документи\PPitStopPlanner\trackDefaults.base.json
```

Base-файл залишається незмінним. Ручні значення пального та VE із сайту або оверлея записуються тільки в `trackDefaults.json`.

Пріоритет значень у наступних розрахунках:

1. ручні локальні значення;
2. особиста історія чистих кіл;
3. preset автомобіля і траси;
4. загальні значення траси.

Live uploader передає лише значення, що відрізняються від базової конфігурації.

### Синхронізація із сайтом

Сайт і локальний застосунок обмінюються даними через live uploader.

- Зміни на сайті тимчасово потрапляють у серверну чергу.
- Uploader отримує команду у відповіді на наступне відправлення телеметрії.
- Відповідний запис у локальному `trackDefaults.json` оновлюється.
- Uploader повертає локальну відмінність на сайт.
- Базова конфігурація ніколи не змінюється.

З'єднання визначається комбінацією Session code та Personal uploader code.

### Менеджерський режим та результати гонок

Менеджерський інтерфейс показує live-інформацію про автомобілі спільної сесії:

- загальні та класові позиції;
- кола й час;
- оцінку запасу пального та VE;
- стан шин;
- піт-стопи та поточний стан у боксах;
- пошкодження;
- індивідуальні деталі стратегії.

Завершені гонки можуть зберігатися в архіві результатів.

### Найкращі кола та рейтинг

Зареєстровані користувачі можуть прив'язати live-сесію та публікувати підтверджені результати LMU. Підтримуються:

- найкращі кола за класом автомобіля і трасою;
- практика, кваліфікація та гонка;
- профілі пілотів;
- погодні умови;
- еталонні рівні темпу;
- публічний рейтинг.

## Локальні дані

Налаштування застосунку та ідентифікатори зберігаються у:

```text
%LOCALAPPDATA%\PPitStopPlanner\
```

Довготривалі користувацькі дані зберігаються у:

```text
Документи\PPitStopPlanner\
```

Оновлення застосунку не перезаписують дані користувача.

## Системні вимоги

- Windows 10 або Windows 11;
- Le Mans Ultimate;
- доступ до LMU shared memory та локального REST API;
- інтернет-з'єднання для синхронізації із сайтом та оновлень.

## Оновлення

Застосунок перевіряє нові версії через GitHub Releases. Під час оновлення замінюються лише програмні файли — локальні налаштування, особиста історія витрати та дані трас зберігаються.
