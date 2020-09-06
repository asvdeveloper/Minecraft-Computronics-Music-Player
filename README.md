# Minecraft-Computronics-Music-Player
"smart" music player work on opencomputers with tape drive from Computronics

Minecraft Computronics Music Player (MCMP)
## Что это?
Способ разметки "кассеты" для удобного перематывания на разные участки и каталогизация музыки. При этом оставив возможность слушать музыку без использования программы.

## Как это устроено?
0. в начале кассеты пишется "MCMP" в 4х байтах(1 буква - 1 байт)(hex вид: `4D 43 4D 50`) как метка для плеера.
1. Пятым байтом пишется версия "разметки".
2. Далее в 2х байтах записываем 16бит число длинны таблицы с описанием данных на ленте(что бы не читать все 16кб области таблицы).
3. Сериализованная таблица с описанием данных на ленте. занимает фиксированные 16384 байт (16Кб)
  - Структура таблицы
  - Таблица содержит нумерованные таблицы для каждого трека
    - В таких субтаблицах  есть следущие поля:
    1. название трека
    2. позиция начала трека относительно начала кассеты
    3. позиция конца трека относительно начала кассеты
    4. скорость воспроизведения кассеты для этого трека
    - длинну можно подсчитать по (`пункт 3` - `пункт 2`)/`пункт 4`/4096 получив дительность в секундах
4. Аудио данные
  - В начале каждого трека присутствуют 4 байта (hex вид: `02 05 00 01`) как метка начала
  - Далее 2 байта номера трека(совпадает с номером в таблице)
  - После сам трек
  - В конце трека должны быть 4 байта (hex вид: `02 05 00 02`) как метка конца.
  - Далее 2 байта номера трека(совпадает с номером в таблице)

## Список задачь: 
- [x] Инициализация баовых переменных и таблиц.
- [x] Служебные функции для упрощения работы.
- [x] Инициализация: чтение и проверка формата "разметки", проверка версии разметки.
- [x] Чтение таблицы содержимого ленты.
- [ ] Проверка содержимого таблицы на соответствие шаблону. (суб таблица "titleItem")
- [ ] (в процессе) Разработка простейшего GUI списка.
- [ ] Разработка управления к GUI.
- [ ] Запись таблицы содержимого ленты.
### Функции плеера
- [ ] Перемотка на выбранный трек.
- [ ] Проверка служебных меток к треку.
- [ ] Установка скорости для трека. 
- [ ] Запись служебных меток.
- [ ] Запись аудио!
- [ ] ...
