# Руководство OpenAPI Шаг 4: объект `paths`

| [*Шаг 1: объект* `openapi`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.5.%20Step%201%20The%20openapi%20object.md) | --> | [*Шаг 2: объект* `info`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.6.%20Step%202%20The%20info%20object.md) | --> | [*Шаг 3: объект* `servers`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.7.%20Step%203%20The%20servers%20object.md) | --> | [**Шаг 4: объект** `paths`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.8.%20Step%204%20The%20paths%20object.md) | --> | [*Шаг 5: объект* `components`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.9.%20Step%205%20The%20components%20object.md) | --> | [*Шаг 6: объект* `security`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.10.%20Step%206%20security%20object.md) | --> | [*Шаг 7: объект* `tags`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.11.%20Step%207%20The%20tags%20object.md) | --> | [*Шаг 8: объект* `externalDocs`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.12.%20Step%208%20The%20externalDocs%20object.md) |

Объект `paths` содержит соль информации нашей API. Объект `paths` имеет несколько подобъектов: [объект элементов пути](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#pathItemObject), [объект операций](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#operationObject) и многое другое.

> Мы двигались со скоростью около 5 км/ч на предыдущих этапах, но здесь мы собираемся разогнаться до 100 км/ч. Ничего страшного, если нет полного понимания следующего контента. Можно вставить пример кода, из этого раздела в Swagger UI, и позже вернуться, чтобы изучить его более подробно.

[Объекты `paths`](#paths)

- [Объекты операций](#operations)

 - [Объект `parameters`](#parameters)

 - [Объект `responses`](#responses)

[Код объекта `paths`](#paths)

[Отображение в Swagger UI](#appearance)

[Примечание о зависимостях параметров](#note)

<a name="paths"></a>
## Объекты `paths`

> Объект `paths` - это та же «конечная точка» в соответствии с терминологии спецификации OpenAPI.

Каждый элемент в объекте `path` содержит [объект операции](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#operation-object). (Операции - это методы GET, POST, PUT и DELETE, которые мы исследовали в разделе [Конечные точки](https://github.com/Starkovden/Documenting_APIs/blob/master/3.%20Documenting%20API%20endpoints/3.4.%20Step%202%20Endpoints%20and%20methods.md) руководства по API.)

Начинаем с перечисления путей (конечных точек) и их разрешенных операций (методов). Для конечной точки `weather` в API OpenWeatherMap есть только один путь (`/weather`) и одна операция (`get`) для этого пути:

    paths:
      /weather:
        get:

<a name="operations"></a>
### Объекты операций

Объект операции ( `get` приведенный выше в коде) содержит различные свойства и объекты:

- `tags`: групповое имя для организации путей в интерфейсе Swagger. Swagger UI сгруппирует конечные точки под заголовками тегов.
- `summary`: краткое описание пути. Swagger UI показывает описание рядом с именем пути. Ограничивают описание только 5-10 словами. Описание отображается и при свернутом разделе.
- `description`: Полное описание пути. Может содержать неограниченное количество деталей. В Swagger UI достаточно места для полного описания.  CommonMark Markdown разрешен.
-  [`externalDocs`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#externalDocumentationObject) (объект): ссылка на документацию с доп.информацией о пути.
- `operationId`: уникальный идентификатор пути.
- [`parameters`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#parameterObject) (объект): Параметры, принимаемые путем. Не включает параметры тела запроса, которые подробно описаны в объекте `requestBody`. Объект `parameters` также может включать в себя [объект `reference`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#referenceObject), который содержит указатель на описание в объекте `components` (этот объект описан на [шаге 5: Объект `components`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.9.%20Step%205%20The%20components%20object.md)).
- [`requestBody`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#requestBodyObject) (объект): детали параметра тела запроса для этого пути. Объект `requestBody` также может включать в себя [объект `reference`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#referenceObject), который содержит указатель на описание в объекте `components` (описание в [шаге 5: Объект `components`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.9.%20Step%205%20The%20components%20object.md)).
- [`response`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#responsesObject) (объект): ответы, предоставленные на запросы по этому пути. Объект `response` также может включать в себя [объект `reference`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#referenceObject), который содержит указатель на описание в объекте `components`. Ответы используют стандартные [коды состояния](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#http-status-codes).
- [`callbacks`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#callbackObject) (объект): детали обратного вызова могут быть инициированы сервером при желании. Callbacks - это операции, выполняемые после завершения выполнения функции. Объект `callbacks` также может включать в себя [объект `reference`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#referenceObject), который содержит указатель на описание в объекте `components`.
- `deprecated`: Является ли путь устаревшим. Можно опустить, если вы не хотите указать устаревшее поле. Boolean.
- [`security`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#securityRequirementObject) (объект): Метод безопасной авторизации, используемый с операцией. Этот объект добавляется на уровне пути, только если нужно перезаписать объект `security` на корневом уровне. Имя определяется объектом `securitySchemes` в объекте `components`. Более подробная информация об этом представлена ​​в [шаге 6: объект `security`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.10.%20Step%206%20security%20object.md).
- [`servers`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#serverObject) (объект): Объект `servers`, который может отличаться от [глобального объекта  `servers`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.7.%20Step%203%20The%20servers%20object.md) для этого пути.

Каждое из вышеупомянутых свойств, имеющих гиперссылку и «(объект)», содержат дополнительные уровни. Их значения не просто типы данных, такие как строки, а скорее объекты, которые содержат свои собственные свойства.

> Несомненно, нужно обращаться к [спецификации OpenAPI](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md), чтобы узнать, какие детали требуются для каждого из значений и объектов. На курсе нет возможности воспроизвести все нужные детали. Здесь просто поверхностное знакомство со свойствами OpenAPI.

Давайте добавим скелет объекта операций к нашему коду:

    paths:
      /weather:
        get:
          tags:
          summary:
          description:
          operationId:
          externalDocs:
          parameters:
          responses:
          deprecated:
          security:
          servers:
          requestBody:
          callbacks:

И удалим несколько ненужных полей, которые нам не нужны для нашей документации по API OpenWeatherMap:

- Нет необходимости включать [объект `requestBody`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#requestBodyObject) потому что ни один путь API OpenWeatherMap не содержит параметров тела запроса.
- Нет необходимости включать [объект `servers`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#serverObject) потому что используется тот же URL глобальных `servers`, который мы определили [глобально на корневом уровне](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.7.%20Step%203%20The%20servers%20object.md).
- Нет необходимости включать [security](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#securityRequirementObject) потому что используется один и тот же объект `security`, который мы определим глобально на корневом уровне позже (см. [Шаг 6: объект security](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.10.%20Step%206%20security%20object.md)).
- Нет необходимости включать `deprecated` потому что ни один из путей не устарел.
- Нет необходимости включать `callbacks` потому что ни один из путей не использует колбэки.

В результате мы можем уменьшить количество соответствующих полей до следующего:

    paths:
      /weather:
        get:
          tags:
          summary:
          description:
          operationId:
          externalDocs:
          parameters:
          responses:

Большинство свойств для объекта операции либо требуют простых строк, либо содержат относительно простые объекты. Наиболее подробный объект здесь - это [объект `parmeters`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.8.%20Step%204%20The%20paths%20object.md#%D0%BE%D0%B1%D1%8A%D0%B5%D0%BA%D1%82-parameters) и [объект `responses`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.8.%20Step%204%20The%20paths%20object.md#%D0%BE%D0%B1%D1%8A%D0%B5%D0%BA%D1%82-responses).         

<a name="parameters"></a>
#### Объект `parameters`

[Объект `parameters`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#parameterObject) содержит массив со следующими свойствами:

- `name`: имя параметра.
- `in`: место параметра. Возможные значения: `header`, `path`, `query`, или `cookie`. (Параметры тела запроса здесь не описаны.).
- `description`: описание параметра.
- `required`: требуется ли параметр.
- `deprecated`: является ли параметр устаревшим.
- `allowEmptyValue`: позволяет ли параметр передавать пустое значение.
- `style`: как данные параметра сериализуются (преобразуются в байты во время передачи данных).
- `explode`: расширенный параметр, связанный с массивами.
- `allowReserved`: разрешены ли зарезервированные символы.
- [`schema`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schemaObject) (объект): Схема или модель для параметра. Схема определяет структуру входных или выходных данных. Обратите внимание, что `schema` также может содержать объект `example`.
- `example`: пример типа носителя. Если объект `example` содержит примеры, эти примеры появляются в Swagger UI, а не в содержимом объекта `example`.
- [`examples`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#exampleObject) (объект): Пример типа носителя, включающий схему.

Вот объект `paths`, который включает детали `parameters`:

    paths:
      /weather:
        get:
          tags:
          - Current Weather Data
          summary: "Call current weather data for one location."
          description: "Access current weather data for any location on Earth including over 200,000 cities! Current weather is frequently updated based on global models and data from more than 40,000 weather stations."
          operationId: CurrentWeatherData
          parameters:
          - name: q
            in: query
            description: "**City name**. *Example: London*. You can call by city name, or by city name and country code. The API responds with a list of results that match a searching word. For the query value, type the city name and optionally the country code divided by a comma; use ISO 3166 country codes."
            schema:
              type: string

          - name: id
            in: query
            description: "**City ID**. *Example: `2172797`*. You can call by city ID. The API responds with the exact result. The List of city IDs can be downloaded [here](http://bulk.openweathermap.org/sample/). You can include multiple cities in this parameter &mdash; just separate them by commas. The limit of locations is 20. *Note: A single ID counts as a one API call. So, if you have city IDs, it's treated as 3 API calls.*"
            schema:
              type: string

          - name: lat
            in: query
            description: "**Latitude**. *Example: 35*. The latitude coordinate of the location of your interest. Must use with `lon`."
            schema:
              type: string

          - name: lon
            in: query
            description: "**Longitude**. *Example: 139*. Longitude coordinate of the location of your interest. Must use with `lat`."
            schema:
              type: string

          - name: zip
            in: query
            description: "**Zip code**. Search by zip code. *Example: 95050,us*. Please note that if the country is not specified, the search uses USA as a default."
            schema:
              type: string

          - name: units
            in: query
            description: '**Units**. *Example: imperial*. Possible values: `standard`, `metric`, and `imperial`. When you do not use the `units` parameter, the format is `standard` by default.'
            schema:
              type: string
              enum: [standard, metric, imperial]
              default: "imperial"

          - name: lang
            in: query
            description: '**Language**. *Example: en*. You can use lang parameter to get the output in your language. We support the following languages that you can use with the corresponded lang values: Arabic - `ar`, Bulgarian - `bg`, Catalan - `ca`, Czech - `cz`, German - `de`, Greek - `el`, English - `en`, Persian (Farsi) - `fa`, Finnish - `fi`, French - `fr`, Galician - `gl`, Croatian - `hr`, Hungarian - `hu`, Italian - `it`, Japanese - `ja`, Korean - `kr`, Latvian - `la`, Lithuanian - `lt`, Macedonian - `mk`, Dutch - `nl`, Polish - `pl`, Portuguese - `pt`, Romanian - `ro`, Russian - `ru`, Swedish - `se`, Slovak - `sk`, Slovenian - `sl`, Spanish - `es`, Turkish - `tr`, Ukrainian - `ua`, Vietnamese - `vi`, Chinese Simplified - `zh_cn`, Chinese Traditional - `zh_tw`.'
            schema:
              type: string
              enum: [ar, bg, ca, cz, de, el, en, fa, fi, fr, gl, hr, hu, it, ja, kr, la, lt, mk, nl, pl, pt, ro, ru, se, sk, sl, es, tr, ua, vi, zh_cn, zh_tw]
              default: "en"

          - name: mode
            in: query
            description: "**Mode**. *Example: html*. Determines the format of the response. Possible values are `xml` and `html`. If the mode parameter is empty, the format is `json` by default."
            schema:
              type: string
                enum: [json, xml, html]
                default: "json"

<a name="responses"></a>
#### Объект `responses`

Другое существенное свойство в объекте операций - это объект `responses`. Для свойства `responses` обычно ссылаются на полное определение в объекте `components`, поэтому рассказ об объекте `responses` в следующем разделе - [Шаг 5. Объект компонентов](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.9.%20Step%205%20The%20components%20object.md). (На этом шаге уже слишком много информации.)

На данный момент, чтобы редактор Swagger проверил и показал наш путь, давайте просто добавим некоторый контент-заполнитель для `responses`:

    responses:
      200:
        description: Successful response
        content:
          application/json:
            schema:
              title: Sample
              type: object
              properties:
                placeholder:
                  type: string
                  description: Placeholder description

    404:
      description: Not found response
      content:
        text/plain:
          schema:
            title: Weather not found
            type: string
            example: Not found

См. [Describing Parameters](https://swagger.io/docs/specification/describing-parameters/) в документации OpenAPI Swagger для более подробной информации.

<a name="paths"></a>
## Код объекта `paths`

Теперь давайте объединим два вышеупомянутых блока кода (и `parameters`, и `responses`) для нашего объекта `paths`. Можем вставить этот код в редактор Swagger, добавляем  наш объект `paths` под кодом `openapi`, `info` и `server`, которые мы добавили в предыдущих уроках.

    paths:
      /weather:
        get:
          tags:
          - Current Weather Data
          summary: "Call current weather data for one location."
          description: "Access current weather data for any location on Earth including over 200,000 cities! Current weather is frequently updated based on global models and data from more than 40,000 weather stations."
          operationId: CurrentWeatherData
          parameters:
          - name: q
            in: query
            description: "**City name**. *Example: London*. You can call by city name, or by city name and country code. The API responds with a list of results that match a searching word. For the query value, type the city name and optionally the country code divided by a comma; use ISO 3166 country codes."
            schema:
              type: string

          - name: id
            in: query
            description: "**City ID**. *Example: `2172797`*. You can call by city ID. The API responds with the exact result. The List of city IDs can be downloaded [here](http://bulk.openweathermap.org/sample/). You can include multiple cities in this parameter &mdash; just separate them by commas. The limit of locations is 20. *Note: A single ID counts as a one API call. So, if you have city IDs, it's treated as 3 API calls.*"
            schema:
              type: string

          - name: lat
            in: query
            description: "**Latitude**. *Example: 35*. The latitude coordinate of the location of your interest. Must use with `lon`."
            schema:
              type: string

          - name: lon
            in: query
            description: "**Longitude**. *Example: 139*. Longitude coordinate of the location of your interest. Must use with `lat`."
            schema:
              type: string

          - name: zip
            in: query
            description: "**Zip code**. Search by zip code. *Example: 95050,us*. Please note that if the country is not specified, the search uses USA as a default."
            schema:
              type: string

          - name: units
            in: query
            description: '**Units**. *Example: imperial*. Possible values: `standard`, `metric`, and `imperial`. When you do not use the `units` parameter, the format is `standard` by default.'
            schema:
              type: string
              enum: [standard, metric, imperial]
              default: "imperial"

          - name: lang
            in: query
            description: '**Language**. *Example: en*. You can use lang parameter to get the output in your language. We support the following languages that you can use with the corresponded lang values: Arabic - `ar`, Bulgarian - `bg`, Catalan - `ca`, Czech - `cz`, German - `de`, Greek - `el`, English - `en`, Persian (Farsi) - `fa`, Finnish - `fi`, French - `fr`, Galician - `gl`, Croatian - `hr`, Hungarian - `hu`, Italian - `it`, Japanese - `ja`, Korean - `kr`, Latvian - `la`, Lithuanian - `lt`, Macedonian - `mk`, Dutch - `nl`, Polish - `pl`, Portuguese - `pt`, Romanian - `ro`, Russian - `ru`, Swedish - `se`, Slovak - `sk`, Slovenian - `sl`, Spanish - `es`, Turkish - `tr`, Ukrainian - `ua`, Vietnamese - `vi`, Chinese Simplified - `zh_cn`, Chinese Traditional - `zh_tw`.'
            schema:
              type: string
              enum: [ar, bg, ca, cz, de, el, en, fa, fi, fr, gl, hr, hu, it, ja, kr, la, lt, mk, nl, pl, pt, ro, ru, se, sk, sl, es, tr, ua, vi, zh_cn, zh_tw]
              default: "en"

          - name: mode
            in: query
            description: "**Mode**. *Example: html*. Determines the format of the response. Possible values are `xml` and `html`. If the mode parameter is empty, the format is `json` by default."
            schema:
              type: string
              enum: [json, xml, html]
              default: "json"

        responses:
          200:
            description: Successful response
            content:
              application/json:
                schema:
                  title: Sample
                  type: object
                  properties:
                    placeholder:
                      type: string
                      description: Placeholder description

        404:
          description: Not found response
          content:
            text/plain:
              schema:
                title: Weather not found
                type: string
                example: Not found

<a name="appearance"></a>
## Отображение в Swagger UI

Отображение `paths` в Swagger UI будет таким:

![paths](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/img/9.png?raw=true)


Чтобы увидеть подробности развернем наш раздел «Current Weather Data». Когда нажмем **Try it out**, вы увидите, что поле заполняется описанием. Если вы хотите, чтобы поле заполнялось значением, добавьте свойство `default`  в схему (как показано с параметром `mode` в приведенном выше коде).

Однако, все параметры не могут быть переданы с одним и тем же запросом - вы используете только те параметры, которые вам нужны для запроса, который вы делаете. (Например, вы не можете передавать почтовый индекс и название города, а также широту / долготу и т.д. в одном запросе.) Поэтому не имеет смысла использовать значения по умолчанию для каждого параметра, поскольку тогда пользователю потребуется удалить большинство из них.

> Swagger UI сворачивает каждый путь по умолчанию. Можно установить, будет ли начальное отображение свернуто или открыто, используя [параметр `docExpansion` в Swagger UI](https://github.com/swagger-api/swagger-ui#parameters). Этот параметр `docExpansion` предназначен для Swagger UI и не является частью спецификации OpenAPI. Swagger UI имеет более [20 различных параметров](https://github.com/swagger-api/swagger-ui#parameters), которые управляют дисплеем. Например, если не хотите, чтобы отображался раздел "Models", нужно добавить параметр `defaultModelsExpandDepth: -1` в файл Swagger UI.

<a name="note"></a>
## Примечание о зависимостях параметров

Спецификация OpenAPI не позволяет объявлять зависимости с параметрами или взаимоисключающими параметрами. В документации Swagger OpenAPI указано:

> OpenAPI 3.0 не поддерживает зависимости параметров и взаимоисключающие параметры. Существует открытый запрос функции по адресу [https://github.com/OAI/OpenAPI-Specification/issues/256](https://github.com/OAI/OpenAPI-Specification/issues/256). Можно задокументировать ограничения в описании параметра и определить логику в ответе 400 Bad Request. ([Parameter Dependencies](https://swagger.io/docs/specification/describing-parameters/#parameter-dependencies-19))

В случае конечной точки погоды с OpenWeatherMap большинство параметров являются взаимоисключающими. Мы не можем выполнять поиск по идентификатору города и почтовому индексу одновременно. Хотя параметры являются необязательными, мы должны использовать хотя бы один параметр. Кроме того, при использовании параметра `lat`, нужно использовать и параметр `lon`, потому что это парные параметры. Спецификация OpenAPI не может программно отражать эту структурированную логику, поэтому мы должны объяснить это в свойстве `description` или в другой, более концептуальной документации.
