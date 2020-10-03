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
    - В таких субтаблицах есть следущие поля:
    1. название трека "t"
    2. позиция начала трека относительно начала кассеты "sp"
    3. позиция конца трека относительно начала кассеты "ep"
    4. скорость воспроизведения кассеты для этого трека "s"
  - длинну можно подсчитать по (`пункт 3` - `пункт 2`)/`пункт 4` получив дительность в байтах. Для получения длительности в секундах небходимо дополнительно разделить на 4096.
4. Аудио данные
  - Предполагается что аудио данные не будут изменятся и дополнятся какими либо метками.

## Установка и использование:
0. Установка 
  - Качаем файл по [ссылке](https://raw.githubusercontent.com/asvdeveloper/Minecraft-Computronics-Music-Player/master/soft/MCMP-1/MCMP.lua) или смотрим в soft/MCMP-х/ где x - версия "разметки".
  - Сохраняем его под именем mcmp.lua(или любым другим, на ваше усмотрение) в папку `/usr/bin/`. Полный путь `/usr/bin/mcmp.lua`.

## Список задач: 
- [x] Инициализация базовых переменных и таблиц.
- [x] Служебные функции для упрощения работы.
- [x] Инициализация: чтение и проверка формата "разметки", проверка версии разметки.
- [x] Чтение таблицы содержимого ленты.
- [x] Проверка содержимого таблицы на соответствие шаблону. (суб таблица "titleItem")
- [x] Таблица абсолютных позиций основных параметров(т.е. formatName, formatVersion, titlesTableLength, titlesTable)
- [x] Служебные функции: Разбивка n бит число на 8битные группы. 
- [x] Служебные функции: Запись на ленту блоками.
- [x] Запись таблицы содержимого ленты.
- [x] Создание новых меток.
- [x] Управление программой параметрами запуска.
### Функции плеера
- [x] Перемотка на выбранный трек.
- [x] Поддержка ввода в секундах/минутах/часах.
- [x] Обратный перевод байт в секудны/минуты/часы.
- [ ] Поддержка "чтения без остановки воспоизведения".
- [ ] Установка скорости для трека. 
- [ ] Запись аудио!
- [ ] Функция дефрагментации: перемещение с целью убрать "пропуски".
- [ ] Функция вспроизведения: воспоизведение с "перемоткой пропусков".
- [ ] ...
