# Структура каталогов и назначение файлов

Назад: Схема работы PHPC • К началу: Документация • Далее: Порядок обработки запроса

Содержание
Панель управления (admin)
Кешированные данные (cache)
Инсталлятор (install)
Языковые данные (language)
Ядро PHP Compiler (phpc)
Плагины и модули (plugins)
Все файлы движка PHP Compiler размещены в шести каталогах:

 admin (Панель управления)
 cache (Кешированные данные)
 install (Инсталлятор)
 language (Языковые данные)
 phpc (Ядро)
 plugins (Плагины и модули)

Основным каталогом является, конечно же, /phpc/. Это ядро PHP Compiler. В нем находится файл index.php, на который посредством файла .htaccess перенаправляются все входящие запросы, и который выполняет всю работу − подключает другие файлы, создает классы, анализирует запрос и собирает готовую страницу.

Панель управления (admin)

В каталоге /admin/ находится все то, что относится к панели управления, или "админке", сайта. Во фронтальной части сайта этот каталог никак не используется, так что если хотите, можете переименовать его во что-нибудь другое. Для только что установленного проекта каталог имеет вид:

 panel.css (Таблица стилей для админки)
 constant.php (Константы для админки)
 controls.php (API панели управления)
 function.php (Дополнительные функции)
 global.php (Общий для всех плагинов скрипт)
 index.php (Главная страница и фреймы админки)
 options.php (Плагин "Настройки")
 phpc.php (Плагин "Управление PHPC")
 panel.png (Логотип PHPC для админки)
 spacer.gif (Прозрачная картинка 1x1)

Файлы panel.css и panel.png − это соответственно таблица стилей админки и логотип сайта, который отображается в верхнем левом углу админпанели. Не стесняйтесь изменить таблицу стилей, чтобы "перекрасить" админку по своему вкусу, либо изменить картинку с логотипом на другую. Картинка должна быть в формате PNG на прозрачном фоне. Вы можете не трогать существующие файлы, а закачать новые в дополнение к старым. Все дополнительные CSS файлы автоматически "подхватываются" панелью и подключаются в текст страницы, а чтобы перенаправить адрес логотипа на новый, достаточно изменить константу AdminLogoLocation.

Файл constant.php − конфигурационный файл админки. Там хранятся различные настройки, относящиеся к ее отображению, которые по тем или иным причинам нельзя вынести в таблицу стилей. Например, вы можете изменить ширину левого фрейма, в котором находится меню (константа AdminFramesMenuWidth), или изменить параметры внешнего WYSIWYG-редактора.

Файл controls.php содержит в себе API-библиотеку движка. Другими словами, там находятся функции, с помощью которых происходит отображение страниц админки. Меню, таблицы, формы, списки, деревья − для всего этого и многого другого предусмотрен набор удобных функций.

Файл function.php содержит функции, которые не относятся к API, но и не имеют отношения к фронтальной части сайта. Функции для установки новых плагинов, для работы со Smart-формами, для поддержки многоязычности в админке − все это находится там.

Файл global.php является вспомогательным для любого плагина панели управления. Он подключает все необходимые библиотеки (включая перечисленные выше), создает глобальные объекты и проверяет авторизацию. Если в админку пытается зайти неавторизованный посетитель, либо срабатывает какая-либо из систем защиты админпанели, файл отображает форму авторизации и немедленно завершает работу скрипта.

Файл index.php − это "домашняя страница" панели управления. Он отвечает за отображение фреймов, главного меню, верхней полоски навигации, а также центральной части страницы − той самой, где выводится приветственная надпись и где расположен верстак с различными полезными возможностями. При необходимости плагины могут дополнять этот верстак своими элементами.

Наконец, файлы options.php и phpc.php − это два базовых плагина, которые поставляются вместе с PHP Compiler. Первый плагин − это Настройки, второй плагин − это Управление PHPC.

Кешированные данные (cache)

Данный каталог предназначен для хранения файлового кеша PHPC.

Файловый кеш используется в случаях, когда для отображения страницы требуются данные, которые слишком накладно рассчитывать каждый раз снова и снова. Такие данные сохраняются в каталоге /cache/ в сериализованном формате, в виде файлов с расширением .dat. Каждая кешированная структура хранит "дату устаревания" − это позволяет кешу автоматически обновляться через какое-то время. Для работы с кешем предусмотрены специальные методы класса Optimizer, кроме того, файловый кеш можно в любой момент очистить вручную из админпанели (Управление PHPC − Очистка кеша).

Для того, чтобы к кешированным данным нельзя было добраться "из внешнего мира", каталог /cache/ защищен файлом .htaccess с директивой Deny from all.

Инсталлятор (install)

В каталоге /install/ находится один файл index.php. Это инсталлятор движка, главная задача которого − помочь разработчику сконфигурировать систему и сохранить все основные настройки в файле config.php каталога /phpc/. После того, как инсталлятор завершил свою работу и сохранил конфигурационный файл, каталог /install/ можно смело удалить − он больше не нужен. Более того, все попытки повторно запустить инсталлятор (в ситуации, когда файл config.php уже существует) автоматически блокируются.

Языковые данные (language)

Каталог /language/ предназначен для хранения сообщений на различных языках. В настоящий момент это русский и английский, но в будущем могут появиться и другие. Для удобства каждому языку дается двухбуквенное обозначение − название локали. Русскому языку соответствует локаль ru, английскому − локаль en. У только что установленного проекта каталог имеет следующую структуру:

 en (Английский язык)
 ru (Русский язык)
 language.php (Базовые данные локализации)

Подкаталог en хранит все сообщения на английском языке, подкаталог ru − на русском. Файл language.php является общим для всех языков.

Когда движок определяет, на каком языке ему следует работать, он просто подключает файл language.php, а затем подключает все PHP-файлы, расположенные в подкаталоге, имя которого совпадает с названием локали. В результате формируется глобальный массив $language, который хранит в себе все языковые данные проекта, и который используется как в админке, так и на самом сайте.

Ядро PHP Compiler (phpc)

В каталоге /phpc/ находятся все жизненно важные для работы сайта классы и библиотеки. В нем также находится файл index.php, который обрабатывает все входящие запросы. При установке системы сюда же сохраняется и конфигурационный файл config.php.

 backcomp.php (Функции для обратной совместимости)
 compiler.php (Класс Compiler)
 config.php (Конфигурационный файл)
 constant.php (Константы движка)
 database.php (Класс Database)
 filesyst.php (Класс FileSystem)
 format.php (Класс Formatter)
 function.php (Библиотека функций, API)
 index.php (Основной файл PHPC)
 language.php (Поддержка многоязычности)
 mailsyst.php (Класс MailSystem)
 optimize.php (Класс Optimizer)

Файл backcomp.php служит для обратной совместимости движка со старыми версиями плагинов. В случае, если какая-то функция или константа меняет свое название (например, старое название было явно неудачным), в этом файле сохраняется ее "двойница" со старым названием. Это позволяет сайтам, в которых использовалось устаревшее название функции, работать как раньше.

Файл compiler.php содержит класс Compiler, наиболее сложный класс во всей системе. Его задача − анализ запроса, формирование данных для вызываемой страницы, компиляция и выполнение шаблонов, обработка специальных тегов. Такие вспомогательные функции, как работа со стилями и сессиями, обслуживание связей между плагинами, генерация ссылок, отображение страниц ошибки или редиректа, также возложены на него.

Файл config.php − конфигурация проекта. Здесь хранятся настройки подключения к БД, язык сайта, ключ шифрования данных и админский пароль. Если вы хотите переопределить какую-либо из стандартных констант движка, также скопируйте ее в файл config.php. Этот файл подключается самым первым, и его определения констант имеют приоритет.

Файл constant.php − различные настройки проекта (константы) по умолчанию, которые обычно можно оставить как есть. Подробное описание этих констант можно найти в разделе: Стандартные константы. Совет: если вам нужно изменить значение какой-либо константы, лучше не изменять ее прямо в файле constant.php, а скопировать ее в файл config.php, где и указать ей новое значение. В будущем, если вы заходите обновить движок до новой версии, измененные значения констант не будут затерты.

Файлы database.php, filesyst.php и mailsyst.php содержат классы Database, FileSystem и MailSystem, которые предназначены для удобной работы с базой данных, файловой системой и электронной почтой, соответственно. Каждому из этих классов посвящен отдельный раздел Документации.

Файл format.php содержит класс Formatter, необходимый для поддержки форматированного текста, т.е. текста, содержащего BB-коды. Поддержка стандартных BB-кодов встроена в движок, и при желании вы можете создавать новые или редактировать существующие коды в панели управления.

Файл function.php − библиотека общих функций движка. Для их описания в Документации также предусмотрен отдельный раздел: Стандартные функции.

Файл index.php − центральный файл движка. Именно он вызывается каждый раз, когда посетитель запрашивает какую-либо страницу вашего сайта. Данный файл подключает все необходимые библиотеки и плагины, создает экземпляры классов, после чего запускает процесс обработки запроса и генерации страницы.

Файл language.php отвечает за многоязычность и за текущий язык проекта. Он определяет текущую локаль и подключает все необходимые файлы локализации, формируя массив $language. Данный файл также содержит несколько полезных функций для работы с локализованными данными.

Наконец, файл optimize.php содержит класс Optimizer, предназначенный для оптимизации и ускорения "узких" мест в системе. Он отвечает за выборку, кеширование и выполнение шаблонов и пакетов, а также содержит методы для удобной работы с файловым кешем.

Плагины и модули (plugins)

В каталоге /plugins/ находятся дополнительные модули движка, которые обычно оформлены как классы. Эти модули могут подключаться к движку как автоматически (посредством константы PhpcPreloadPlugins), так и вручную, через поле "список плагинов" в свойствах пакета. По умолчанию в этом каталоге находятся три файла:

 colorer.php (Подсветка синтаксиса)
 nested.php (Работа с деревьями Nested Sets)
 zipfile.php (Поддержка файлов ZIP)

Файл colorer.php содержит класс SyntaxColorer с набором удобных методов для подсветки синтаксиса в пакетах и шаблонах PHPC. Чтобы увидеть, как он работает, зайдите в панель управления, откройте список шаблонов вашего проекта и щелкните по любой ссылке "Просмотр". Класс корректно подсвечивает не только теги HTML, но и специальные теги PHPC.

Файл nested.php содержит класс NestedSet с набором простых, но эффективных методов для работы с деревьями произвольной вложенности. Класс позволяет хранить такие деревья в базе данных (поддерживается даже режим "мульти-деревья", когда в одной таблице хранится сразу много деревьев), оптимизировать данные в них, быстро выбирать данные дерева − полностью или частично, а также быстро превращать линейную структуру данных в рекурсивную для использования в шаблонах, при помощи метода prepareSelection.

Наконец, файл zipfile.php содержит класс ZipFile с набором методов для упаковки файла или файлов в ZIP-архивы. Для работы этому классу не требуются никакие дополнительные библиотеки.

Назад: Схема работы PHPC • К началу: Документация • Далее: Порядок обработки запроса