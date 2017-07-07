# Простые примеры

Назад: Шаблонизатор • К началу: Документация • Далее: Наследование шаблонов

Эти примеры показывают, как в PHPC можно вставлять шаблоны друг в друга при помощи тега <insert:>, как при этом передавать параметры и использовать такую удобную возможность, как обертывание шаблонов (wrapping).

Пример 1

Нужно разместить на странице две одинаковые формы авторизации − слева вверху и справа внизу.

Шаблон htmlLoginForm:

<form action="/actionUsers" method="post">
<input type="hidden" name="action" value="login">
Ваш ник: <input type="text" name="username"><br>
Пароль: <input type="password" name="password"><br>
<input type="submit">
</form>
Шаблон страницы:

<!-- Верхняя левая часть страницы -->
<insert:htmlLoginForm/>

...

<!-- Нижняя правая часть страницы -->
<insert:htmlLoginForm/>
Обратите внимание на косую черту в конце специального тега − она является обязательной в данном случае. Без нее PHPC будет считать, что вы указали только открывающий тег insert, но забыли про закрывающий, и выдаст сообщение об ошибке.

Пример 2

Нужно разместить декорированный блок с внутренним содержимым, чтобы его оформление не смешивалось с содержанием.

Шаблон htmlBlock:

<table border="1">
  <tr>
    <td>Заголовок блока</td>
  </tr>
  <tr>
    <!-- Содержимое блока -->
    <td><var:content></td>
  </tr>
</table>
Шаблон страницы:

<!-- Между открывающим и закрывающим тегами insert пишем содержимое блока -->
<!-- Оно будет подставлено на место тега var:content в шаблоне htmlBlock -->

<insert:htmlBlock>

Наша пища должна быть:
<ul>
  <li>Вкусной</li>
  <li>Здоровой</li>
</ul>

</insert:htmlBlock>
Пример 3

Нужно разместить друг под другом два или более декорированных блока, с разными заголовками и с разным содержимым.

Измененный шаблон htmlBlock:

<!-- Этому шаблону можно передать параметр title (заголовок) -->

<table border="1">
  <tr>
    <!-- Заголовок блока -->
    <td><var:title></td>
  </tr>
  <tr>
    <!-- Содержимое блока -->
    <td><var:content></td>
  </tr>
</table>
Шаблон страницы:

<!-- Вставляем первый блок -->
<insert:htmlBlock title="Первый блок">

Содержимое <b>первого</b> блока.

</insert:htmlBlock>

...

<!-- Вставляем второй блок -->
<insert:htmlBlock title="Второй блок">

Содержимое <i>второго</i> блока.

</insert:htmlBlock>
Пример 4

Нужно разместить все тот же декорированный блок, с формой авторизации внутри него.

Шаблон страницы:

<insert:htmlBlock title="Войти">
  <insert:htmlLoginForm/>
</insert:htmlBlock>
Здесь один шаблон вставляется внутрь другого. PHPC поддерживает произвольную вложенность вставки шаблонов друг в друга, просто не забывайте про парность тегов и про теги <var:content> в текстах этих шаблонов. Допускаются даже такие экзотические конструкции:

<insert:htmlBlock title="Первый уровень">
  <insert:htmlBlock title="Второй уровень">
    <insert:htmlBlock title="Третий уровень">
    ...
    </insert:htmlBlock>
  </insert:htmlBlock>
</insert:htmlBlock>
Хотя на практике такое встречается редко.

Пример 5

Нужно быстро собрать красиво оформленное пользовательское меню.

Шаблон страницы:

<insert:htmlMenuGroup title="Навигация">
  <insert:htmlMenuItem link="/" title="На главную"/>
  <insert:htmlMenuItem link="/chat" title="Чат"/>
  <insert:htmlMenuItem link="/forum" title="Форум"/>
  <insert:htmlMenuItem link="/gallery" title="Галерея"/>
  <insert:htmlMenuItem link="/library" title="Библиотека"/>
</insert:htmlMenuGroup>

<insert:htmlMenuGroup title="Программы">
  <insert:htmlMenuItem link="/opensource" title="Открытые"/>
  <insert:htmlMenuItem link="/freeware" title="Бесплатные"/>
  <insert:htmlMenuItem link="/software" title="Условно-бесплатные"/>
</insert:htmlMenuGroup>
Вспомогательные шаблоны оформляйте по своему вкусу. :)

Шаблон htmlMenuGroup:

<b><var:title></b>
<hr>
<ul>
<var:content>
</ul>
Шаблон htmlMenuItem:

<li><a href="<var:link>"><var:title></a></li>

Назад: Шаблонизатор • К началу: Документация • Далее: Наследование шаблонов