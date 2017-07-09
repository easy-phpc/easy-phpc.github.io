# Стандартные константы

Назад: Методы класса Optimizer • К началу: Документация • Далее: Прочее

Содержание
Базовые константы
Имена COOKIE-параметров
Сессии
Компрессия HTML
Файловый кеш и файловые данные
База данных
Обработка запроса
Кеширование данных
Почта
Интервалы времени
Атрибуты и маски
Прегенерация HTML
Практически все стандартные константы PHP Compiler находятся в файле constant.php каталога /phpc/. Это облегчает поиск нужной константы, если вам нужно посмотреть ее текущее значение или изменить его на новое.

Еще раз напоминаю, что конфигурационный файл движка (файл config.php) подключается к системе самым первым, еще до файла с константами. Поэтому те константы, которые нужно переопределить новыми значениями, лучше скопировать в этот файл, поскольку в таком случае они будут иметь приоритет. Например:

// Автоматически подключить модули Каптчи и Пользователей
// Эту строку желательно добавить в файл /phpc/config.php
define("PhpcPreloadPlugins","captcha,users");
Рассмотрим стандартные константы PHPC подробнее.

Базовые константы

define("PhpcLocalesList","en,ru");
define("PhpcLocale","ru");
define("PhpcPreloadPlugins","");
PhpcLocalesList: список локалей через запятую, которые известны системе. Должен совпадать со списком подкаталогов каталога /language/, или являться его подмножеством.
PhpcLocale: для обычных (не-многоязычных) проектов данная константа хранит название локали − языка проекта, автоматически блокируя все прочие локали. Для многоязычных проектов данная константа должна содержать пустую строку.
PhpcPreloadPlugins: список плагинов (файлов из каталога /plugins/, без указания расширения) через запятую, автоматически подключаемых к системе. Порядок перечисления имен имеет значение. Файлы подключаются директивой require_once.
Следующие четыре константы являются опциональными − они не обязательно должны быть определены. Если какая-либо константа из нижеперечисленных не определена, используется значение по умолчанию:

define("PhpcRoot","/");
define("PhpcSuffix","");
define("PhpcPreferredFolder","");
define("PhpcPreferredLocale","");
PhpcRoot: ссылка на главную страницу сайта, или, другими словами, корневой каталог сайта. Если сайт, как и положено, установлен в корневой каталог хоста, в этой константе нет необходимости. Если сайт устанавливается в подкаталог (что не рекомендуется), константа должна быть определена и иметь формат "/folder/subfolder/", то есть начинаться со слеша и заканчиваться им же.
PhpcSuffix: "расширение" ссылок на страницы сайта. По умолчанию в этой константе нет необходимости, поскольку страницы PHPC не имеют расширения. Если вам нужно придать страницам сайта вид типа "page.html", эта константа должна иметь значение ".html".
PhpcPreferredFolder: нужно ли добавлять к ссылкам, созданным при помощи метода createLink класса Compiler, дополнительный префикс-каталог. Обычно в этом нет нужды (и поэтому в константе нет необходимости), но в редких случаях, вроде многоязычных сайтов, разнесенных по различным виртуальным каталогам, с сайтом по умолчанию, находящимся не в корневом каталоге, эта константа может быть полезна.
PhpcPreferredLocale: какая локаль является для данного проекта предпочтительной. Эта константа имеет смысл только для многоязычных проектов, и имеет приоритет над набором предпочтительных языков, которые посетитель передает заголовком HTTP-Accept-Language. Учтите, что остальные методы определения локали − выбор локали через имя домена (ru.mysite.org), выбор локали через виртуальный каталог (mysite.org/ru/index), передача предпочтительной локали в куках − имеют более высокий приоритет, чем эта константа.
Имена COOKIE-параметров

define("PhpcPasswordParam","phpcpassword");
define("PhpcPasswordCookie","phpcpassword");
define("PhpcLocaleCookie","phpclocale");
define("PhpcStyleCookie","phpcstyle");
define("PhpcSessionCookie","phpcsession");
define("PhpcMemberNameParam","phpcmembername");
define("PhpcMemberPassParam","phpcmemberpass");
define("PhpcMemberNameCookie","phpcmembername");
define("PhpcMemberPassCookie","phpcmemberpass");
PhpcPasswordParam: имя параметра для передачи пароля в форме авторизации.
PhpcPasswordCookie: имя параметра для хранения зашифрованного пароля.
PhpcLocaleCookie: имя параметра для хранения выбранного пользователем языка.
PhpcStyleCookie: имя параметра для хранения выбранного пользователем стиля.
PhpcSessionCookie: имя параметра для хранения ID сессии пользователя.
PhpcMemberNameParam: имя параметра "логин" для авторизации в member-панели.
PhpcMemberPassParam: имя параметра "пароль" для авторизации в member-панели.
PhpcMemberNameCookie: имя параметра для хранения имени пользователя.
PhpcMemberPassCookie: имя параметра для хранения зашифрованного пароля пользователя.

Сессии

define("PhpcSessionEnabled",false);
define("PhpcSessionUseCookies",true);
define("PhpcSessionUseURLs",false);
define("PhpcSessionCleanup",false);
define("PhpcSessionCatchEnabled",true);
define("PhpcSessionCatchRestrictions","");
define("PhpcSessionCatchLimit",10);
define("PhpcSessionTimeout",600);
define("PhpcSessionGCProbability",1);
define("PhpcSessionGCDivisor",100);
define("PhpcSessionParamsLimit",200);
PhpcSessionEnabled: включен ли механизм сессий.
PhpcSessionUseCookies: передавать ли ID сессии через cookie.
PhpcSessionUseURLs: передавать ли ID сессии через адрес.
PhpcSessionCleanup: использовать ли метод UsersSupport::processSessionCleanup для постобработки устаревших сессий (значение true), или такие сессии можно просто удалять из таблицы (значение false).
PhpcSessionCatchEnabled: можно ли "подхватывать" сессии, то есть брать для посетителя, который не прислал корректный ID сессии, одну из существующий сессий для того же IP адреса.
PhpcSessionCatchRestrictions: список полей таблицы sessions через запятую, которые обязательно должны быть пустыми (или равными 0), для того, чтобы эту сессию можно было "подхватить". Другими словами, список "приватных" данных сессии, доступ к которым есть только у посетителей, приславших правильный ID сессии.
PhpcSessionCatchLimit: количество записей таблицы sessions, которые выбираются для попытки "подхвата" сессии. Подробнее о механизме "подхвата" сессий в PHPC написано в статье: Обработка сессий в PHPC.
PhpcSessionTimeout: интервал в секундах, после которого необновившаяся сессия считается устаревшей.
PhpcSessionGCProbability, PhpcSessionGCDivisor: числитель и знаменатель для значения вероятности запуска сборщика мусора в сессиях. По умолчанию вероятность равна 1/100 = 0,01.
PhpcSessionParamsLimit: максимальная длина строки, в которой сохраняется список наиболее важных параметров запроса. Полученная строка хранится в поле params таблицы sessions, и используется для сервисов типа "кто и где сейчас на сайте".
Компрессия HTML

define("OutputCompressionEnabled",true);
define("OutputCompressionLevel",1);
OutputCompressionEnabled: включено ли автоматическое GZIP-сжатие готовых HTML-страниц.
OutputCompressionLevel: степень сжатия (от 1 до 9). По умолчанию минимальна, чтобы не нагружать сервер.
Файловый кеш и файловые данные

define("FileCacheEnabled",true);
define("FileCacheFilename","/cache/%s.dat");
define("FileSystemUserAgent","Mozilla/5.0 (compatible)");
define("FileSystemTimeout",10);
FileCacheEnabled: включен ли механизм файлового кеширования.
FileCacheFilename: маска, указывающая путь к файлам кеша и их расширение.
FileSystemUserAgent: значение заголовка User-Agent для отправки запросов на другие серверы.
FileSystemTimeout: максимальное время ожидания ответа от других серверов в секундах.
База данных

define("DatabaseQueryLogEnabled",false);
define("DatabaseStartupQueries","");
define("DatabaseRestrictedTables","adminlog,memberlog");
DatabaseQueryLogEnabled: разрешить ли логирование запросов к БД (в целях отладки, например).
DatabaseStartupQueries: список дополнительных "стартовых" запросов к БД, разделенных символом ";".
DatabaseRestrictedTables: список таблиц через запятую, которые нежелательно отображать в общем списке.
Обработка запроса

define("CompilerExpose",true);
define("CompilerEfficientSlashes",false);
define("CompilerSecureCookies",true);
define("CompilerNoCacheHeaders",true);
define("CompilerAntispamEnabled",true);
define("CompilerRecodeRequest",false);
define("CompilerRecodeSpaces",false);
define("CompilerRecodePreserve","\w\x80-\xff/");
define("CompilerRequestSymbols","\w\x80-\xff%");
define("CompilerIndexPage","index");
define("CompilerErrorPage","404");
define("CompilerComplexInherit","bundles,params");
define("CompilerPluginFilename","/plugins/%s.php");
define("CompilerEchoLimit",10);
CompilerExpose: можно ли посылать посетителю HTTP-заголовок "X-Generated-By" с версией PHPC.
CompilerEfficientSlashes: можно ли оптимизировать работу функции slashes, экранируя только одинарные кавычки, но не экранируя двойные (значение true), или же делать это необязательно (значение false). Если включить данную настройку, PHPC будет генерировать чуть более "опрятные" дампы данных, но функция slashes будет работать чуть медленнее.
CompilerSecureCookies: если данная настройка включена, то отправка кук через функцию phpcsetcookie будет происходить с передачей HTTP-атрибута "HttpOnly". Это делает все переданные куки невидимыми для сценариев JavaScript и делает сайт более устойчивым к XSS-атакам.
CompilerNoCacheHeaders: нужно ли посылать заголовки No-Cache для сгенерированных HTML-страниц.
CompilerAntispamEnabled: разрешить ли простое шифрование e-mail адресов при их выводе в шаблоне.
CompilerRecodeRequest: разрешить ли автоматическое конвертирование строки запроса (Request URI) из UTF-8 в кодировку сайта. Полезно для сайтов с адресами на русском языке. Включая эту настройку, помните о том, что запросы на русском требуют намного больше места для хранения (из-за конвертирования сначала в UTF-8, а потом в формат WWW-URL-Encoded), например, строка "Привет" в формате строки запроса будет иметь вид "%D0%9F%D1%80%D0%B8%D0%B2%D0%B5%D1%82". Большинство браузеров умеют отображать такие строки правильно, но не все.
CompilerRecodeSpaces: разрешить ли автоматическую замену символа подчеркивания "_" на символ пробела в запросах и обратно. Эти две настройки влияют на работу функций phpcurlencode и phpcurldecode.
CompilerRecodePreserve: набор символов, которые не нужно никак кодировать при конвертировании строки в формат строки запроса.
CompilerRequestSymbols: набор символов, которые, если идут друг за другом в строке запроса, нужно считать частью одного параметра при анализе и разборе "красивой ссылки". Обратите внимание, что дефис ("-") не входит в этот набор, то есть символ дефиса по умолчанию разбивает строку на несколько отдельных параметров. Например, в строке "2010-01-01" будет найдено три параметра − год, месяц и день.
CompilerIndexPage: имя страницы, которая используется для отображения главной страницы сайта.
CompilerErrorPage: имя страницы, которая используется для обработки ситуации "страница не найдена".
CompilerComplexInherit: набор полей таблицы pages, для наследования которых от одной PHPC-страницы к другой используется более сложное правило, чем обычное "если значение не указано, берем его из предка".
CompilerPluginFilename: маска, указывающая путь к плагинам PHPC и их расширение.
CompilerEchoLimit: максимальная длина текста для упрощенного вывода в шаблонизаторе.
Кеширование данных

define("CompilerCacheEnabled",true);
define("CompilerCacheCombined",false);
define("CompilerCacheTemplateNames",false);
define("CompilerCacheCompressionEnabled",true);
define("CompilerCacheCompressionLevel",1);
define("CompilerCacheTables","cachetemplates,cachebundles");
CompilerCacheEnabled: разрешено ли кеширование скомпилированных шаблонов и пакетов.
CompilerCacheCombined: нужно ли очистке кеша компилятора также очищать и файловый кеш.
CompilerCacheTemplateNames: нужно ли при компиляции шаблонов сохранять данные об их именах.
CompilerCacheCompressionEnabled: разрешено ли хранение скомпилированных данных в сжатом виде.
CompilerCacheCompressionLevel: степень сжатия данных при сохранении кеша.
CompilerCacheTables: список таблиц через запятую, в которых хранится кеш компилятора. Эти таблицы автоматически очищаются при внесении каких-либо изменений в шаблоны/пакеты проекта, а также при вызове метода clearCache класса Optimizer.
Почта

define("MailHeadersNewline","\n");
define("MailMessageNewline","\n");
define("MailDebuggerEnabled",false);
define("MailDebuggerFilename","/mail/%s.txt");
MailHeadersNewline: последовательность символов, которая используется для разделения строк в заголовке формируемого письма. По умолчанию используются Unix-переносы, поскольку такой вариант правильно воспринимается бóльшим числом почтовых серверов.
MailMessageNewline: аналогичная последовательность, но для содержимого письма.
MailDebuggerEnabled: разрешена ли отладка почты. При включенном режиме отладки все отправляемые письма, вместо отправки на почтовый сервер, сохраняются в виде файлов, в каталоге /mail/.
MailDebuggerFilename: куда сохранять письма при включенном режиме отладки.
Интервалы времени

define("OneMinute",60);
define("OneHour",3600);
define("OneDay",86400);
define("OneWeek",604800);
define("OneMonth",2592000);
define("OneYear",31536000);
Несколько констант для использования в классах и пакетах. Значение каждой константы указано в секундах.

Атрибуты и маски

define("FolderCreateAttributes",0777);
define("EmailAddressPattern","{^\w[\w\-.]*@\w[\w\-]*\.[\w\-.]*\w\$}");
define("UploadSafeExtensions",".gif,.jpg,.jpeg,.png");
FolderCreateAttributes: набор атрибутов в восьмеричной нотации (значение начинается с 0), которые указываются новому каталогу при его создании методом createFolder класса FileSystem. Если ваша файловая система настроена как надо и скрипты PHP, запускаясь, получают все необходимые права доступа к файлам, то обычно нет необходимости давать новым каталогам так много прав. В этом случае, возможно, имеет смысл переопределить константу значением 0755 или даже 0700.
EmailAddressPattern: регулярное выражение для проверки корректности присланного e-mail адреса.
UploadSafeExtensions: набор типов файлов через запятую, разрешенных к загрузке на сервер.
Прегенерация HTML

define("PredefinedLocalhost","127.0.0.1");
define("PredefinedChop"," .,:;-!?([{/\t\r\n");
define("PredefinedDots","...");
define("PredefinedNewline","<br>");
define("PredefinedWrap","<wbr>");
define("PredefinedParagraphOpen","<p>");
define("PredefinedParagraphClose","</p>");
define("PredefinedLinkDefault","<a href=\"%s\">%s</a>");
define("PredefinedLinkTarget","<a href=\"%s\" target=\"%s\">%s</a>");
define("PredefinedCode","<div class=\"code\">%s</div>");
define("PredefinedOptionDefault","<option value=\"%s\">%s</option>");
define("PredefinedOptionSelected","<option value=\"%s\" selected=\"selected\">%s</option>");
define("PredefinedOptionGroup","<optgroup label=\"%s\">%s</optgroup>");
Набор констант, связанных с работой специальных тегов и с генерацией текста HTML-страницы. Первая константа используется для различения ситуации "сайт работает локально" и "сайт работает на продукционном сервере", и используется функцией isLocalhost. Остальные константы используются при выводе форматированного текста и типичных HTML-конструкций в шаблонах. Подробнее об этом написано в статье: Специфические функции вывода.

Назад: Методы класса Optimizer • К началу: Документация • Далее: Прочее