# Добавление, редактирование и удаление данных

Назад: Методы класса Database • К началу: Документация • Далее: Выборка данных

Содержание
addLine
addLineStrict
modifyField
incrementField
decrementField
modifyLine
modifyLines
deleteLine
deleteLines
getCounterValue
Далее перечислены методы класса Database, предназначенные для добавления новых записей в таблицы, для редактирования существующих записей и для удаления данных из таблиц. Рассмотрим их подробнее.

addLine

bool addLine ( string table, array values [, bool replace] )

Метод добавляет новую запись в таблицу table. Данные задаются ассоциативным массивом values (ключи − названия полей в произвольном порядке, значения − добавляемые данные). Экранирование данных выполняется автоматически, вам не нужно заботиться о корректности выполняемого запроса. По умолчанию используется тип вставки INSERT, но если указать true в качестве третьего параметра, будет использован метод вставки REPLACE. Метод возвращает true или false в зависимости от того, удалось ли добавить новую запись.

Если в таблице table есть поле-счетчик, то есть поле с атрибутом AUTO_INCREMENT, то указывать ему значение при добавлении записи не нужно. Оно будет присвоено записи автоматически, а узнать это значение сразу после добавления можно при помощи метода getCounterValue.

При добавлении данных не обязательно указывать значения всех полей таблицы. Можно перечислить в массиве values лишь часть полей − недостающие поля получат значения по умолчанию, и запись все равно будет добавлена. Допускается даже указать параметру values пустой массив, хотя на практике такой вариант встречается редко.

Пример:

// Добавление нового альбома в таблицу music
$values=array(
  "band"=>"Nightwish",
  "album"=>"Angels Fall First",
  "tracks"=>8);
$database->addLine("music",$values);
addLineStrict

bool addLineStrict ( string table, array values [, bool replace] )

Метод работает аналогично предыдущему, с одним отличием: если добавить новую запись не удалось, метод не возвращает значение false, а генерирует фатальную ошибку и немедленно завершает работу скрипта. Полезно при добавлении критических данных или при выполнении критически важных операций с данными, когда возникает ситуация "данные должны быть добавлены в любом случае".

Пример:

// Добавление нового пользователя, после всех проверок
$values=array(
  "username"=>$username,
  "password"=>sha1($password));
$database->addLineStrict("users",$values);
modifyField

bool modifyField ( string table, string field, mixed value [, string conditions] )

Метод изменяет значение поля field на новое значение value у записи в таблице table, удовлетворяющей условиям conditions. Новое значение может иметь произвольный тип − целочисленный, вещественный, строковый или логический. Движок экранирует значение поля автоматически при выполнении запроса. Запись (строка таблицы table), которая будет обновлена, определяется параметром conditions − этот параметр должен иметь вид условия в SQL-формате. Если значение параметра conditions не указано, будет затронута первая запись таблицы.

Метод возвращает true, если запись была успешно отредактирована, и false в противном случае.

Пример:

// Изменение количества дорожек у альбома
// Обратите внимание, как правильно подставлять строки в условия
$album="Angels Fall First";
$database->modifyField("music","tracks",10,"album=".slashes($album));
incrementField

bool incrementField ( string table, string field [, string conditions [, int delta]] )

Метод увеличивает значение поля field на заданную величину у записи в таблице table, удовлетворяющей условиям conditions. Величина задается необязательным параметром delta, если он не указан − значение увеличивается на 1.

Пример:

// Увеличение количества просмотов альбома
$album="Angels Fall First";
$database->incrementField("music","views","album=".slashes($album));
decrementField

bool decrementField ( string table, string field [, string conditions [, int delta]] )

Метод работает аналогично предыдущему, с той лишь разницей, что он уменьшает значение поля field. Как и раньше, разница задается необязательным параметром delta, если он не указан − значение уменьшается на 1.

Пример:

// Уменьшение количества инвайтов у пользователя
$userid=10;
$database->decrementField("users","invites","id=$userid AND invites>0");
modifyLine

bool modifyLine ( string table, array values [, string conditions] )

Метод изменяет значения полей у записи в таблице table, удовлетворяющей условиям conditions. Список изменяемых полей и их новые значения указывается ассоциативным массивом values (ключи − названия полей в произвольном порядке, значения − сохраняемые данные). Значения полей экранируются автоматически. Метод возвращает true или false в зависимости от того, удалось ли обновить запись.

Если условие, переданное параметром conditions, удовлетворяет двум или более записям таблицы, будет затронута только первая по счету запись. В частности, если параметр conditions не указан или указана пустая строка, будет затронута только самая первая запись таблицы. Если вам нужно изменить сразу несколько записей таблицы, воспользуйтесь методом modifyLines.

Пример:

// Изменение данных альбома
$album="Century Child";
$newvalues=array(
  "band"=>"Nightwish",
  "genre"=>"Metal",
  "year"=>2002,
  "tracks"=>11);
$database->modifyLine("music",$newvalues,"album=".slashes($album));
modifyLines

void modifyLines ( string table, array values [, string conditions] )

Метод работает аналогично предыдущему, с одним важным отличием: он может изменить несколько записей сразу. Кроме того, он не возвращает результата. Если условие, переданное параметром conditions, удовлетворяет одновременно нескольким записям таблицы, у всех них будут отредактированы данные, соответственно параметру values. В частности, если параметр conditions не указан или указана пустая строка, будет затронута вся таблица.

Пример:

// Пометка всех дорогих товаров, как "популярные" и как "хит продаж"
$minimalPrice=10000;
$newvalues=array("popular"=>true,"hit"=>true);
$database->modifyLines("products",$newvalues,"price>=$minimalPrice");

// Удаление неиспользованных инвайтов у всех пользователей
$database->modifyLines("users",array("invites"=>0));
deleteLine

bool deleteLine ( string table [, string conditions] )

Метод удаляет запись из таблицы table, удовлетворяющую условиям conditions. Метод возвращает true или false в зависимости от того, удалось ли удалить запись (запись иногда бывает невозможно удалить, если она связана с записями в другой таблице).

Если условие, переданное параметром conditions, удовлетворяет двум или более записям таблицы, будет удалена только первая по счету запись. В частности, если параметр conditions не указан или указана пустая строка, будет удалена только самая первая запись таблицы. Если вам нужно удалить сразу несколько записей таблицы, воспользуйтесь методом deleteLines.

Пример:

// Удаление альбома
$album="Seven Lives Many Faces";
$database->deleteLine("music","album=".slashes($album));
deleteLines

void deleteLines ( string table [, string conditions] )

Метод работает аналогично предыдущему, с одним важным отличием: он может удалить несколько записей сразу. Кроме того, он не возвращает результата. Если условие, переданное параметром conditions, удовлетворяет одновременно нескольким записям таблицы, они все будут удалены. В частности, если параметр conditions не указан или указана пустая строка, из таблицы будут удалены все данные, так что будьте осторожны.

Если вы хотите очистить таблицу, то есть удалить из таблицы все записи, рекомендуется пользоваться методом clearTable. Он работает гораздо быстрее, чем deleteLines без параметра conditions.

Пример:

// Удаление всех альбомов группы Enigma
$band="Enigma";
$database->deleteLines("music","band=".slashes($band));

// Удаление всех пользователей, не имеющих комментариев
$database->deleteLines("users","comments=0");
getCounterValue

int getCounterValue ( void )

Если вы только что добавили новую запись в таблицу, и одно из полей этой таблицы имеет атрибут AUTO_INCREMENT (счетчик), то этому полю при добавлении записи значение присваивается автоматически. Данный метод предназначен для того, чтобы узнать значение, которое было присвоено только что добавленной записи. Он возвращает либо целочисленное значение поля, либо 0, если предыдущая операция не была операцией добавления или произошла какая-либо ошибка.

Пример:

// Добавление нового товара
$values=array(
  "title"=>"Фотоаппарат Canon",
  "brand"=>"Canon",
  "price"=>5000);
$database->addLine("products",$values);
// Получение значения ID у только что созданного товара
$productid=$database->getCounterValue();

Назад: Методы класса Database • К началу: Документация • Далее: Выборка данных