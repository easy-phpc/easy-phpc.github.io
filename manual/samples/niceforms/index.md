# Пример создания красивых форм

Назад: Пример создания выпадающего меню • К началу: Документация • Далее: Пример создания формы обратной связи

В этом примере речь пойдет об оформлении различных форм на сайте. Если у вас сложный, динамический проект, в котором формы ввода данных − обычное явление, и дизайн сайта требует, чтобы они были стильно оформлены, значит, данный пример − для вас.

Обычно формы − самая "некрасивая" часть на сайте: логика форм сама по себе требует солидного количества HTML-тегов, а в сочетании с оформлением страницы все это может привести к мешанине в тегах и путанице. Попробуем исправить положение. Идея простая: вынесем все оформление во вспомогательные теги, чтобы вызывать их по мере надобности, а также разделим форму на независимые элементы.

Для начала выполните два несложных шага:

1. Скачайте и распакуйте архив по этой ссылке. Внутри находится один файл (forms-templates.sql), это набор дополнительных шаблонов для форм. Импортируйте его в панели управления (Управление PHPC − Импорт БД). В списке шаблонов должно появиться несколько новых элементов.

2. Скачайте архив по второй ссылке. Распакуйте его в корневую папку вашего проекта с сохранением структуры каталогов, это набор изображений для обрамления форм. Убедитесь, что в папке вашего сайта появился подкаталог images, а в нем − подкаталог forms.

Теперь приступим к экспериментам. Откройте любой подходящий шаблон и добавьте в него фрагмент:

<insert:formMain title="Вход в систему" page="actionUser" action="login">
  <insert:formInput title="Имя:" name="username"/>
  <insert:formPassword title="Пароль:" name="password"/>
</insert:formMain>
Откройте эту страницу в браузере. Должно получиться что-то вроде этого:

Как видите, достаточно простой фрагмент кода отображает прилично оформленную форму, причем если нажать на кнопку отправки, данные будут отправлены на страницу "actionUser", а помимо собственно данных формы (поля "username" и "password"), будет также отправлен скрытый параметр "action" со значением "login". Все эти значения указаны в параметрах тегов и вы можете задавать их по своему желанию.

В данном случае форма состоит из двух элементов: поле ввода (шаблон formInput) и поле ввода пароля (шаблон formPassword). Второе отличается от первого только тем, что на экране вместо данных отображаются звездочки. Для обоих полей, а также для самой формы, указан еще один параметр − "title". Это заголовок формы/поля.

Рассмотрим более сложный пример:

<?php
$styleOptions=array(
  "classic"=>"Классический стиль",
  "modern"=>"Стиль \"Модерн\"",
  "lite"=>"Лайт-версия");
?>

<insert:formMain title="Регистрация нового участника" page="actionUser" action="register">
  <insert:formInput title="Имя участника:" name="username"/>
  <insert:formPassword title="Пароль:" description="Не менее 5 символов." name="password"/>
  <insert:formPassword title="Повторите пароль:" name="password2"/>
  <insert:formInput title="E-mail адрес:" name="email" value="webmaster@yoursite.ru"/>
  <insert:formTextarea title="Примечания:" name="notes"/>
  <insert:formChooser title="Выберите стиль:" name="style" options=styleOptions/>
  <insert:formYesNo title="Подписаться на рассылку:" name="subscribe"/>
</insert:formMain>
На экране это должно выглядеть примерно так:

Главные отличия по сравнению с предыдущим вариантом: используется больше разных элементов, кроме параметра "title" у одного элемента есть параметр "description" (краткое описание поля, если нужно), у еще одного элемента есть параметр "value" (начальное значение поля), а в самом низу есть выпадающий список. Для выпадающего списка (шаблон formChooser), кроме прочего, необходим список возможных значений в виде ассоциативного массива. Этот массив формируется в PHP-вставке в начале примера, а потом передается шаблону параметром "options". Разумеется, список возможных значений можно формировать и в пакете, например, выбирать из базы данных:

$usergroups=$database->getLines("usergroups");
$usergroupOptions=extractArrayColumns($usergroups,"id","title");
Как видите, ничего сложного. Если интересно, можете посмотреть у себя исходный текст страницы с формой и сравнить объем HTML-кода с фрагментом выше. Вы удивитесь! :)

Назад: Пример создания выпадающего меню • К началу: Документация • Далее: Пример создания формы обратной связи