# Основные преимущества PHPC

Назад: Введение в PHPC • К началу: Документация • Далее: Установка и настройка
Содержание
Компактность
Быстродействие
Стабильность
Завершенность
Удобство для разработчика
Удобство для пользователя
Бесплатность
Компактность

Главное отличие PHP Compiler от других фреймворков − его компактность. Все ядро движка хранится в десятке файлов, в одном каталоге /phpc/ и занимает не более 200 Кб − где еще вы такое увидите? При этом в движке реализованы все необходимые функции, его базового функционала вполне достаточно для потребностей большинства современных сайтов.

Быстродействие

Как естественное следствие компактности, PHPC очень быстро работает. Я уже говорил о том, что у PHPC нет конкурентов по части быстродействия среди полноценных фреймворков, и готов повторить это еще раз. Даже такие разработки, как CodeIgniter, которые заслуженно гордятся своими небольшими размерами ("всего-то" 200 файлов) и хорошей скоростью работы, все равно проигрывают PHPC в быстродействии. И это не просто пузомерка. Быстро и эффективно работающий движок означает меньшую нагрузку на сервер, меньшее потребление системных ресурсов. Чтобы запустить даже высокопосещаемый сайт на PHPC, вам не придется покупать для него отдельный сервер. Достаточно обойтись VDS или даже скромным shared-хостингом, а это − экономия денег.

Стабильность

PHPC имеет стабильный код. Это фреймворк с раз навсегда продуманной архитектурой, и выбрав его однажды, вы не рискуете в один прекрасный день столкнуться с ситуацией "автор движка решил все перелопатить подвергнуть рефакторингу, а что же теперь делать мне?" Практически все новые версии PHPC являются стабильными в том смысле, что последующие версии, выходящие уже после них, не требуют немедленного обновления, судорожного затыкания дыр в безопасности, припрятывания неразумных архитектурных решений и т. д. Нет. Движок продуман раз и навсегда, и новые версии лишь привносят новый функционал, не перечеркивая старый. Даже если в один день разработка PHPC прекратится навсегда, у вас по-прежнему останется стабильная, работающая версия.

Завершенность

В отличие от многих других фреймворков, в PHPC вам нет необходимости дорабатывать что-либо напильником, редактировать под свои нужды файл index.php или даже писать свой собственный код, который потом становится частью ядра. Это ни к чему. Движок уже написан за вас, он готов к работе. Вы можете сразу приступать к созданию своего проекта, не тратя время на то, чтобы сначала подогнать фреймворк под требования будущего сайта.

Удобство для разработчика

В процессе создания нового сайта на PHPC нет ничего сложного, даже для новичка. В отличие от некоторых "объектно-ориентированных" фреймворков, где создание каждой новой страницы усложнено до предела (от вас требуется создать десять новых каталогов, разместить в них всевозможные классы-модели, "вьюхи", контроллеры, которые еще надо сначала написать, а также файлы с шаблонами − и все это ради одной новой страницы на сайте, неужели вам не жалко собственного времени и сил?), PHPC предоставляет разработчику панель управления и удобный веб-интерфейс для создания структуры будущего сайта и управления ей впоследствии.

Необычно? Да, это необычно. Вы привыкли к тому, что удобный интерфейс для работы с сайтом предоставляется лишь конечному заказчику, а программист всегда остается человеком "второго сорта", который вынужден снова и снова писать новые классы и ковырять существующие, закачивать файлы через FTP, в общем, выполнять обязанности Золушки. Забудьте об этом. PHP Compiler предоставляет удобные средства для управления не только контентом сайта (как это реализовано во многих системах класса CMS), но и его структурой. Как следствие, поднимать сайт с нуля становится на порядок проще.

Удобство для пользователя

Панелью управления PHPC может пользоваться не только разработчик, но и заказчик проекта, и даже конечный клиент. Движок предоставляет простые, но эффективные средства для разграничения доступа к панели управления сайтом, а также для пополнения ее новыми функциями и модулями. API админпанели − это набор простых, удобных, стильных функций. С их помощью вы создадите систему управления контентом вашего сайта, простую и понятную, максимально заточенную под вашу область интересов.

Бесплатность

PHP Compiler совершенно бесплатен и распространяется по лицензии LGPL (Lesser GPL), что дает вам право использовать движок для создания любых сайтов, в том числе и коммерческих для получения прибыли. В отличие от лицензии GPL, лицензия LGPL дает вам право сохранять все ваши разработки в тайне. Кроме того, никто не обязывает вас размещать у себя ссылку на домашнюю страницу движка, как того требуют некоторые CMF/CMS. Конечно, такая ссылка горячо приветствуется, но ставить ее или нет − целиком на ваше усмотрение.

Назад: Введение в PHPC • К началу: Документация • Далее: Установка и настройка