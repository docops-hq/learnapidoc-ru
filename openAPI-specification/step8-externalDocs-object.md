# Руководство OpenAPI Шаг 8: Объект `externalDocs`

| [*Шаг 1: объект* `openapi`](step1-openapi-object.md) | --> | [*Шаг 2: объект* `info`](step2-info-object.md) | --> | [*Шаг 3: объект* `servers`](step3-servers-object.md) | --> | [*Шаг 4: объект* `paths`](step4-paths-object.md) | --> | [*Шаг 5: объект* `components`](step5-components-object.md) | --> | [*Шаг 6: объект* `security`](step6-security-object.md) | --> | [*Шаг 7: объект* `tags`](step7-tags-object.md) | --> | [**Шаг 8: объект** `externalDocs`](step8-externalDocs-object.md) |

[Объект `externalDocs`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#external-documentation-object) позволяет добавлять ссылки на внешнюю документацию. Можно добавлять ссылки на внешние документы в объекте `paths`.

[Пример объекта `externalDocs`](#example)

[Отображение в Swagger UI](#appearanse)

[Итоговый результат](#finish)

<a name="example"></a>
## Пример объекта `externalDocs`

Вот пример объекта `externalDocs`:

    externalDocs:
      description: API Documentation
      url: https://openweathermap.org/api

Обратите внимание, что эта документация должна относиться в целом к API. Чтобы связать определенный параметр с дополнительной документацией, можно добавить объект `externalDocs` к объекту операции, как отмечено в описании [Объектов операций](step4-paths-object.md#%operations) в Шаге 4: Объект `paths`.

<a name="appearanse"></a>
## Отображение в Swagger UI

Добавим приведенный выше код к корневому уровню документа OpenAPI в интерфейсе Swagger.

В Swagger UI после описания API появится ссылка вместе с информацией об API:

![externaldoc](img/18.png)

> Ссылка на внешнюю документацию

На данный момент, мы можем догадаться о некоторых проблемам интеграции Swagger UI с остальной частью нашей документации. Скорее всего, будет два вывода и полуфрагментированный пользовательский опыт. Объект `externalDocs` обеспечивает предсказуемое место для ссылки [концептуальных разделов](../conceptual-topics/README.md). См. [Интеграция Swagger UI со сторонними документами](integrating-swagger-with-docs.md) для получения дополнительной информации о стратегиях интеграции.

<a name="finish"></a>
## Итоговый результат

Теперь, когда мы выполнили все шаги в руководстве OpenAPI, мы закончили создание нашего документа спецификации OpenAPI. Итоговый вариант спецификации здесь: [https://idratherbewriting.com/learnapidoc/docs/rest_api_specifications/openapi_openweathermap.yml](https://idratherbewriting.com/learnapidoc/docs/rest_api_specifications/openapi_openweathermap.yml)

Вот как выглядит собранная в Swagger UI спецификация:

![final](img/19.png)
