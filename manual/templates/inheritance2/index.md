# Подробнее о наследовании

Назад: Наследование шаблонов • К началу: Документация • Далее: Комментарии

Наследование шаблонов осуществляется в PHPC при помощи тега <area:>. После двоеточия должен следовать идентификатор на английском, который указывает имя переопределяемой области. В одном шаблоне может переопределяться сразу несколько областей, для их различения и нужен идентификатор. Как вы уже видели по предыдущей статье, самый распространенный случай − это наследование шаблона страницы с переопределением ее центральной части. В этом случае принято использовать имя "content", а тег выглядит как <area:content>.

Пример 1. Пометка центральной части страницы в базовом шаблоне:

<html>
<body>
<area:content>

<!-- Если хотите, можно указать содержимое центральной части и для базового шаблона. -->
<!-- Оно отобразится в случае, если вы забудете переопределить ее в производном шаблоне. -->
<!-- Если же вы ее переопределите − этот текст будет вырезан, и заменен новым. -->

Извините, страница находится в разработке.

</area:content>
</body>
</html>
Переопределяться может несколько фрагментов сразу, при условии, что у разных фрагментов разные идентификаторы. Более того, переопределяемые фрагменты могут быть вложенными друг в друга (но при этом не должны частично перекрывать друг друга, то есть либо фрагменты идут отдельно друг от друга, либо один фрагмент находится целиком внутри другого фрагмента).

Пример 2. Пометка нескольких фрагментов страницы:

<html>
<head>
<area:header>

<!-- HTML-заголовок страницы по умолчанию -->
<!-- Если в одном из дочерних шаблонов вы захотите добавить новые HTML-заголовки, -->
<!-- например, добавить HTML-редирект, достаточно переопределить область area:header -->

<title><var:currentPage:title></title>

</area:header>
</head>
<body>
<area:content>

<!-- Центральная часть страницы по умолчанию -->
Добро пожаловать на сайт!

</area:content>

<!-- Дополнительный "слот" для подвала страницы -->
<!-- На случай, например, добавления JS-обработчиков после загрузки страницы -->
<!-- По умолчанию здесь пусто, поэтому спецтег имеет краткую форму (слеш в конце) -->

<area:footer/>

</body>
</html>
В дочернем (т.е. наследуемом) шаблоне страницы можно переопределить одну или несколько помеченных выше областей. Синтаксис − точно такой же, как и у базового шаблона. Если какая-то область не переопределена − используется базовый вариант. Если в наследуемом шаблоне вообще ничего не переопределено, он будет вести себя в точности, как базовый шаблон.

Обработка наследования в шаблонах − одна из самых приоритетных операций при компиляции страницы в PHPC. Выше нее только удаление шаблонных комментариев (о них далее). Все остальные операции − обработка специальных тегов и вывод данных − происходят только после того, как движок разобрался с наследованием шаблонов и удалил из текста страницы все оставшиеся теги <area:>.

Назад: Наследование шаблонов • К началу: Документация • Далее: Комментарии