# Пример создания двухуровнего меню

Назад: Пример создания простого сайта • К началу: Документация • Далее: Пример создания разворачивающегося меню

Допустим, мы хотим сделать несложное меню, которое будет отображаться на всех страницах сайта. Пункты будут сгруппированы в разделы, текущая страница должна выглядеть в меню по-другому ("активная"). Для создания такого меню нам не придется ничего программировать, достаточно возможностей встроенного шаблонизатора.

Шаг 1. Добавляем будущее меню в дизайн сайта

Откройте содержимое шаблона htmlDesign и в подходящем месте добавьте фрагмент:

<insert:menu/>
Этот тег вставляет в дизайн сайта другой шаблон (menu). Если попытаться зайти на сайт прямо сейчас, компилятор выдаст сообщение об ошибке, так как такого шаблона у нас еще нет.

Шаг 2. Создаем меню

Создайте новый шаблон с именем menu и следующим содержимым:

<insert:htmlMenu>

<insert:htmlMenuGroup title="Сайт">
  <insert:htmlMenuItem link="/" title="Главная"/>
  <insert:htmlMenuItem link="/news" title="Новости"/>
  <insert:htmlMenuItem link="/about" title="О сайте"/>
</insert:htmlMenuGroup>

<insert:htmlMenuGroup title="Мультимедиа">
  <insert:htmlMenuItem link="/images" title="Картинки"/>
  <insert:htmlMenuItem link="/music" title="Музыка"/>
  <insert:htmlMenuItem link="/video" title="Видео"/>
</insert:htmlMenuGroup>

</insert:htmlMenu>
Данный шаблон будет хранить структуру меню, без оформления. Все оформление будет храниться в отдельных вспомогательных шаблонах − htmlMenu, htmlMenuGroup и htmlMenuItem. Осталось только создать их.

Шаг 3. Создаем вспомогательные шаблоны

Создайте друг за другом еще три шаблона.

Шаблон htmlMenu:

<var:content>
Шаблон htmlMenuGroup:

<table border="1">
<tr><td><var:title></td></tr>
<tr><td><var:content></td></tr>
</table>
Шаблон htmlMenuItem:

<logic:equal property=_SERVER:REQUEST_URI value=link>
<li><b><var:title></b></li>
</logic:equal>

<logic:notEqual property=_SERVER:REQUEST_URI value=link>
<li><a href="<var:link>"><var:title></a></li>
</logic:notEqual>
Первый шаблон хранит оформление меню в целом. Поскольку в нашем примере меню никак не оформлено, этот шаблон пуст (за исключением тега, подставляющего его контент − часть шаблона menu между открывающим и закрывающим тегами).

Второй шаблон хранит оформление группы меню. В нем использован тег <var:title> для вывода названия группы. Название передается при вызове шаблона.

Третий шаблон хранит оформление элемента меню. В нем использовано два условных тега − один срабатывает для активного элемента, другой − для неактивного. PHPC не поддерживает конструкцию типа if...then...else в шаблонах, поэтому условие приходится продублировать. В обоих случаях значение серверной переменной REQUEST_URI (то есть текущий запрос) сравнивается со значением параметра link (адрес ссылки у элемента меню).

Шаг 4. Смотрим, что получилось

Если теперь зайти на сайт, должно отобразиться что-то вроде этого:



Текущая страница отображается в меню жирным текстом и без ссылки.

Теперь, если вам необходимо изменить оформление меню, достаточно изменить шаблоны htmlMenu, htmlMenuGroup либо htmlMenuItem, а если вы хотите добавить в меню новые пункты или изменить существующие − отредактируйте шаблон menu.

Количество групп и количество элементов в группе может быть любым.

Назад: Пример создания простого сайта • К началу: Документация • Далее: Пример создания разворачивающегося меню