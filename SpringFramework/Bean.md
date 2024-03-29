# Бин (Bean)
В Spring объекты, формирующие основу приложения и управляемые контейнером Spring IoC, называются bean-компонентами.  

**Компонент** — это объект, который создается, собирается и управляется контейнером Spring IoC. Грубо говоря, **bean-компонент** — это просто один из многих объектов вашего приложения. Бины и зависимости между ними отражаются в метаданных конфигурации, используемых контейнером. 

### Область видимости (scope) бинов
|             | Scope         | Описание                                                                              | Создание                      | Потокобезопасность |
| ----------- | ------------- | ------------------------------------------------------------------------------------- | ----------------------------- | ------------------ |
| **Default** | singleton     | Все запросы к этому бину будут возвращать один и тот же объект, который кэшируется.   | Сразу при сканировании        | Да                 | 
|             | prototype     | При каждом запросе из контейнера будет возвращаться другой экземпляр.                 | Только после запроса (Lazy)   | Нет                |

\
**Доступные только для web-aware application**
|             | Scope         | Описание                                                                              | Создание                      | Потокобезопасность |
| ----------- | ------------- | ------------------------------------------------------------------------------------- | ----------------------------- | ------------------ |
|             | request       | Область видимости — 1 HTTP запрос.                                                    | На каждый запрос              |                    |
|             | session       | Область видимости — 1 сессия.                                                         | На каждую сессию              |                    |
|             | application   | Область видимости — жизненный цикл ServletContext.                                    |                               |                    |
|             | websocket     | Область видимости — жизненный цикл WebSocket.                                         |                               |                    |

> Область видимости указывается с помощью аннотации @Scope на @Bean методах.
```Java 
@Bean
@Scope("prototype")
public Person personPrototype() {
    return new Person();
}
```
> Чтобы указать способ инициализации, можно использовать аннотацию @Lazy. Она ставится на @Bean-методы, на @Configuration-классы, или на @Component-классы. В зависимости от параметра(true или false), который принимает аннотация, инициализация будет или ленивая, или произойдет сразу. По умолчанию(т.е. без указания параметра) используется true.