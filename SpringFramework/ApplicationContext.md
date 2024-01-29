# Application Context и контейнер

Основа Spring Framework — контейнер, где "живут" объекты.
Контейнер обычно создает множество объектов на основе их конфигураций и управляет их жизненным циклом от создания объекта до его уничтожения.

<div style="text-align:center">
<img src="./images/SpringContainerBasic.png" width="300" height="auto">
</div>

**Контейнер** — это объект, который реализует интерфейс *ApplicationContext*.

**ApplicationContext** — это главный *интерфейс* в Spring-приложении, который предоставляет информацию о конфигурации приложения. Он доступен только для чтения во время выполнения, но может быть перезагружен (reload) при необходимости, если это поддерживает приложение.

Интерфейс **ApplicationContext** обеспечивает:
* фабричные методы бина для доступа к компонентам приложения, наследуя от `ListableBeanFactory`
* возможность загружать файловые ресурсы в общем виде, наследуя от `org.springframework.core.io.ResourceLoader`
* возможность публиковать события и регистрировать обработчики на них, наследуя от `ApplicationEventPublisher`
* возможность работать с сообщениями с поддержкой интернационализации, наследуя от `MessageSource`
* наследование от родительского контекста (1)

> (1) Определения в контексте-потомке всегда будут иметь приоритет. Это означает, например, что один родительский контекст может использоваться всем веб-приложением, в то время как каждый сервлет имеет свой собственный дочерний контекст, независимый от контекста любого другого сервлета.

### Реализации интерфейса ApplicationContext (виды контекста):
* `ClassPathXmlApplicationContext` - читает файл из пути к классам, который должны находиться в папке классов данного приложения или в папке lib в jar
```Java
ApplicationContext context = new ClassPathXmlApplicationContext("applicationcontext/account-bean-config.xml");
```
* `FileSystemXmlApplicationContext` - загружает файл конфигурации XML из файловой системы или из URL-адреса
```Java
String path = "C:/myProject/src/main/resources/applicationcontext/account-bean-config.xml";

ApplicationContext context = new FileSystemXmlApplicationContext(path);
```
* `GenericGroovyApplicationContext` - загружает Groovy-файл конфигурации
```Java
ApplicationContext context = new GenericGroovyApplicationContext("org/myapp/applicationContext.groovy");
```
* `AnnotationConfigApplicationContext` - берет классы, аннотированные метаданными `@Configuration`, `@Component` и JSR-330 в качестве входных данных
```Java
ApplicationContext context = new AnnotationConfigApplicationContext(AccountConfig.class);
```
* и даже `StaticApplicationContext` - настройка контекста через программный доступ из Java, т.е. определение всего контекста через Java-код
* и многие другие


Метод run() в ApplicationContext используется для настройки контекста. 