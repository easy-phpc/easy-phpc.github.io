# Маленькие хитрости

Назад: Установка сторонних скриптов • К началу: Документация

Набор различных приемов, делающих процесс разработки сайта на PHPC еще более простым и удобным.

1. Если у вас одноязычный проект, вы можете смело удалить из проекта неиспользуемые локали. Например, если ваш сайт только на русском языке, вы можете удалить из проекта весь подкаталог en каталога language − эти файлы все равно не используются системой.

2. Если у вас проект на русском и английском языках, и в английской версии вы не используете символы с ударениями типа á, ó, то имеет смысл вручную подредактировать файл language/en/common_en.php, заменив строку

```$language["charset"]="windows-1252";```

на

```$language["charset"]="windows-1251";```

Это не совсем правильно, но очень удобно − даже если вы зайдете в админскую панель под английской локалью, все данные на русском все равно будут отображаться правильно.

3. Независимо от того, на каком языке у вас взведен проект, вы всегда можете пользоваться HTML-кодами для отображения различных "трудновводимых" символов. Например:

&copy; превращается в © (значок авторского права);
&reg; превращается в ® (значок зарегистрированной марки);
&trade; превращается в ™ (значок торговой марки);
&laquo; превращается в « (левая "ёлочка");
&raquo; превращается в » (правая "ёлочка");
&plusmn; превращается в ± (плюс-минус);
&sup1; превращается в ¹ (первая степень);
&sup2; превращается в ² (вторая степень);
&sup3; превращается в ³ (третья степень);
&deg; превращается в ° (градус);
&times; превращается в × (умножение в формулах);
&minus; превращается в − (длинное тире);
&plusmn; превращается в ± (плюс-минус).
и так далее. Здесь можно найти подробный список HTML-кодов.

Такие коды корректно работают в любом месте системы.

4. Если вы храните свой проект в двух экземплярах − дома и на хостинге, и вам требуется время от времени синхронизировать файлы, обычно с этим не возникает проблем. Но файл phpc/config.php, как правило, различается на локальной машине и на сервере, так как там и там разные параметры подключения к БД. Но есть способ обойти и это, и использовать один конфигурационный файл, в котором будут храниться параметры подключения как к локальной БД, так и к базе данных сервера. Соответствующий фрагмент файла config.php при этом выглядит примерно так:

```$localhost=$_SERVER["SERVER_ADDR"]=="127.0.0.1";

define("DatabaseHost","localhost");
define("DatabaseName",$localhost?"local_db":"server_db");
define("DatabaseUser",$localhost?"local_user":"server_user");
define("DatabasePass",$localhost?"local_pass":"server_pass");```

5. Делайте "красивую" ссылку на главную страницу сайта. Если адрес вашего сайта − скажем, www.mysite.ru, то и ссылка "на главную" должна выглядеть как www.mysite.ru, а не www.mysite.ru/index. В том случае, если для создания ссылок вы используете тег <write:link> или <write:anchor>, ссылка на страницу index формируется как надо автоматически. Если же вы просто пишете ссылку в шаблоне, например, так:

<a href="/index">На главную</a>

то более правильным вариантом будет такой:

<a href="/">На главную</a>

6. Если в вашем проекте накопилось много шаблонов, и из длинного списка трудно выбрать нужный, используйте группы шаблонов. Просто создайте новую группу − она ни на что не влияет, кроме отображения списка шаблонов в админке − и укажите ей подходящее название (например, "Шаблоны новостей") и префикс (например, "news"). Все шаблоны, имя которых начинается с этого префикса, будут сгруппированы в отдельный разворачивающийся список.

Точно так же можно поступить со списком страниц и пакетов.

7. Держите свой проект в чистоте. Имеется в виду файловая система − по мере того, как ваш проект растет, вы закачиваете в него все новые и новые картинки и файлы, и если заранее не подумать о структуре размещения данных на сервере, ваш сайт очень быстро превратится в файловую помойку.

Как этого избежать? Лично я пользуюсь несколькими несложными правилами:

Никогда ничего не закачивайте в корневой каталог! В корневом каталоге сайта должен находиться файл .htaccess и ничего более.
Не бойтесь использовать длинные пути к файлам. Адрес "/images/design/header.gif" ничем не хуже адреса "/header.gif", но гораздо понятнее.
Храните данные разного типа раздельно. Грамотным стилем считается создание папки images для хранения изображений, audio для хранения музыки, video для хранения видео, files для хранения файлов или архивов для скачивания и так далее. Конкретные имена папок не имеют значения − если не нравятся эти, вы можете придумать любые другие. Главное, чтобы вам самим было легко определить, что где должно находиться.
Структурируйте ваши ресурсы. Даже если вы решили использовать папку images для хранения всех картинок вашего проекта, это не значит, что нужно все новые картинки закачивать прямо в эту папку. Создайте подпапку images/design для хранения оформления сайта, подпапку images/banners для ваших баннеров, подпапку images/gallery для картинок галереи и т. д. В идеале сама папка images должна всегда оставаться пустой.

Назад: Установка сторонних скриптов • К началу: Документация