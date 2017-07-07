# Пример создания выпадающего меню

Назад: Пример создания разворачивающегося меню • К началу: Документация • Далее: Пример создания красивых форм

Допустим, нам нужно сделать выпадающее меню на сайте − горизонтальную полосу со списком элементов, причем если навести курсор на любой из них, отображается выпадающий список вложенных элементов. Что-то наподобие такого:

Это достаточно просто. Разберем процесс по шагам:

1. Скачайте архив по этой ссылке. Распакуйте его. Внутри находится один файл (dropdownmenu-templates.sql). Это набор дополнительных шаблонов для нашего проекта.

2. Импортируйте этот файл в панели управления (Управление PHPC − Импорт БД). В списке шаблонов проекта должно появиться 5 новых шаблонов:

htmlMenu (оформление горизонтальной полосы меню);
htmlMenuGroup (оформление главного элемента меню);
htmlMenuItem (оформление выпадающего элемента меню);
htmlMenuScripts (набор скриптов для работы меню);
htmlMenuStyles (таблица стилей).
3. Создайте в панели управления новый шаблон menu:

<insert:htmlMenu>

<insert:htmlMenuGroup link="/section1" title="Первый раздел">
  <insert:htmlMenuItem link="/page1" title="Первый документ"/>
  <insert:htmlMenuItem link="/page2" title="Второй документ"/>
  <insert:htmlMenuItem link="/page3" title="Третий документ"/>
</insert:htmlMenuGroup>

<insert:htmlMenuGroup link="/section2" title="Второй раздел">
  <insert:htmlMenuItem link="/page4" title="Четвертый документ"/>
  <insert:htmlMenuItem link="/page5" title="Пятый документ"/>
</insert:htmlMenuGroup>

<insert:htmlMenuGroup link="/section3" title="Пустой раздел" empty/>

</insert:htmlMenu>
Как видите, мы просто вызываем вспомогательные шаблоны, формируя список главных и выпадающих элементов, при этом передавая им названия страниц и ссылки, а вспомогательные шаблоны уже берут на себя всю работу по созданию готового HTML.

Также обратите внимание на последний вызов htmlMenuGroup ("Пустой раздел"). У этого раздела нет вложенных элементов − это допускается, поэтому мы не стали писать пару "открывающий/закрывающий тег" для него, а оформили его как комбинированный (со слешем в конце тега). Кроме того, желательно передать ему дополнительный параметр "empty" без значения, чтобы при наведении на него не отображался пустой список выпадающих элементов.

4. Откройте шаблон htmlDesign, и в подходящем месте добавьте фрагмент:

<insert:menu/>
5. Зайдите на сайт и убедитесь, что меню появилось и работает.

Помните, что как внешнее оформление меню, так и его содержимое, остаются целиком на ваше усмотрение. Если вы хотите "причесать" его внешний вид − смело редактируйте шаблоны htmlMenuXxx (в простейшем случае будет достаточно настроить таблицу стилей). Если вы хотите добавить в меню новые пункты или изменить существующие − редактируйте шаблон menu.

Назад: Пример создания разворачивающегося меню • К началу: Документация • Далее: Пример создания красивых форм