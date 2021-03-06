# Методы класса Compiler

Назад: Методы класса MailSystem • К началу: Документация • Далее: Методы для чтения данных

Основное назначение класса Compiler − компиляция шаблонов и генерирование окончательного HTML-кода страницы перед ее отправкой клиенту. Для того, чтобы сборка страницы работала быстро, все шаблоны транслируются в специальный компактный PHP-код, который сохраняет весь функционал и всю динамику, что была в исходном шаблоне, но выполняется гораздо быстрее. Этот код сохраняется в кеше (таблица cachetemplates) для повторного использования.

Экземпляр класса Compiler создается в движке автоматически и доступен через глобальную переменную $compiler. В пакетах эта переменная доступна автоматически, ее не нужно никак объявлять. В функциях и методах классов ее нужно предварительно объявить командой:

global $compiler;
Большая часть методов класса является служебными, и вызывать их напрямую требуется редко. Как правило, для работы с компилятором вполне хватает методов createLink и captureTemplate − для создания ссылки на страницу и для быстрой сборки шаблона (например, для отправки письма), а также методов standardError и standardRedirect − для отображения стандартного сообщения об ошибке и для красивой переадресации с одной страницы на другую.

Все методы класса можно разделить по смыслу на следующие группы:

Методы для чтения данных
Методы для обработки запроса
Методы для компиляции шаблонов
Прочие методы

Назад: Методы класса MailSystem • К началу: Документация • Далее: Методы для чтения данных