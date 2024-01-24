# Внедрение зависимостей (Dependency Injection)

Когда класс **А** использует класс/интерфейс **B**, тогда **А** зависит от **B**. Класс А не может выполнить свою работу без **B**, и **А** не может быть переиспользован без переиспользования **B**. В таком случае класс **А** называют ***зависимым***, а класс/интерфейс **B** называют ***зависимостью***. 

=> **B является "зависимостью", потому что A "зависим" от B.**

Зависимости могут *"внедряться"* в конструктор объекта, отсюда и возникает термин **"внедрение** (прим. перев.: или иначе — инъекция) **зависимостей"**. 

Внедрение зависимостей не ограничено конструкторами, поэтому можно внедрять зависимости используя методы-сеттеры, либо прямо через публичные поля (что нежелательно). 

> **Внедрение зависимостей (Dependency Injection or DI)** - это стиль конфигурации объекта, при котором поля задаются внешней сущностью. Другими словами, объекты настраиваются внешней сущностью. 

Контейнер выполняет разрешение зависимостей компонентов следующим образом: 
* ApplicationContext создается и инициализируется метаданными конфигурации, описывающими все компоненты. Метаданные конфигурации могут быть указаны с помощью XML, кода Java или аннотаций. 

* Для каждого bean-компонента его зависимости выражаются в форме свойств, аргументов конструктора или аргументов статического фабричного метода (если вы используете его вместо обычного конструктора). Эти зависимости предоставляются компоненту при его фактическом создании. 

* Каждый аргумент свойства или конструктора представляет собой фактическое определение устанавливаемого значения или ссылку на другой компонент в контейнере. 

* Каждый аргумент свойства или конструктора, являющийся значением, преобразуется из указанного формата в фактический тип этого свойства или аргумента конструктора. По умолчанию Spring может преобразовать значение, предоставленное в строковом формате, во все встроенные типы, такие как int, long, String, boolean и т. д. 

Контейнер Spring проверяет конфигурацию каждого компонента при создании контейнера. Однако сами свойства компонента не устанавливаются до тех пор, пока компонент не будет фактически создан. Bean-компоненты с одноэлементной областью действия и настроенные на предварительное создание экземпляров (по умолчанию) создаются при создании контейнера. Области определяются в Bean Scopes. В противном случае компонент создается только тогда, когда он запрошен. Создание bean-компонента потенциально приводит к созданию графа bean-компонентов, поскольку создаются и назначаются зависимости bean-компонента и его зависимостей (и т. д.). Обратите внимание, что несоответствия разрешения между этими зависимостями могут проявиться позднее, то есть при первом создании затронутого компонента. 