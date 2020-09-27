# Руководство OpenAPI Шаг 5: Объект `components`

| [*Шаг 1: объект* `openapi`](step1-openapi-object.md) | --> | [*Шаг 2: объект* `info`](step2-info-object.md) | --> | [*Шаг 3: объект* `servers`](step3-servers-object.md) | --> | [*Шаг 4: объект* `paths`](step4-paths-object.md) | --> | [**Шаг 5: объект** `components`](step5-components-object.md) | --> | [*Шаг 6: объект* `security`](step6-security-object.md) | --> | [*Шаг 7: объект* `tags`](step7-tags-object.md) | --> | [*Шаг 8: объект* `externalDocs`](step8-externalDocs-object.md) |

Объект `components` уникален среди других объектов в спецификации OpenAPI. В `components` хранятся переиспользуемые определения, которые могут появляться в нескольких местах в документе спецификации. В нашем сценарии документации API мы будем хранить детали для объектов `parameters` и `responses` в объекте `components`.

[Причины использования объекта `components`](#reasons)

[Объекты в `components`](#objects)

[Переиспользование параметров в нескольких путях](#reuseParams)

[Переиспользование объектов `responses`](#reuseObjects)

[Описание схемы](#schema)

[Способ обмануть - автоматически генерировать схему из JSON, используя Stoplight](#cheat)

[Использование GUI редакторов для работы с кодом спецификации](#gui)

[Отображение в Swagger UI](#appearanse)

[Раздел Models - почему он существует, как его скрыть](#models)

[Определения `security`](#security)

<a name="reasons"></a>
## Причины использования объекта `components`

Описание деталей параметров и схемы сложных ответов может быть наиболее сложным аспектом спецификации OpenAPI. Хотя можно определить параметры и ответы непосредственно в объектах параметров и ответов, как правило, они не перечисляются там по двум причинам:

- Возможно, будет желание переиспользовать части этих определений в других запросах или ответах. Обычно один и тот же параметр или ответ используется в нескольких местах в API. С помощью объекта `components` OpenAPI позволяет вам повторно использовать одни и те же определения в нескольких местах.
- Возможно, не захочется загромождать свой объект `paths` слишком большим количеством параметров и подробностей ответа, поскольку объект `paths` уже и так сложен из-за нескольких уровней объектов.

Вместо перечисления схемы для ваших запросов и ответов в объекте `paths`, для более сложных схем (или для схем, которые повторно используются в нескольких операциях или путях), используется [объект `reference`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#referenceObject)  (со ссылкой `$ref`), который указывает на конкретное определение в [объекте `components`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#componentsObject). (Подробнее о `$ref` см. В разделе [Использование `$ref`](https://swagger.io/docs/specification/using-ref/).)

Объект `components` можно представить как о приложении к документу, в котором предоставлены данные для повторного использования. Если несколько частей спецификации имеют одну и ту же схему, можно указывать ссылку на один и тот же объект в объекте `components`, и при этом вы получаете единый источник контента. Объект `components` может даже храниться в [отдельном файле](http://apihandyman.io/writing-openapi-swagger-specification-tutorial-part-8-splitting-specification-file/), для более простой организации информации в больших API. (онлайн-редактор Swagger не позволяет использовать несколько файлов для проверки содержимого.)

<a name="objects"></a>
## Объекты в `components`

В объекте `components` можно хранить множество различных переиспользуемых объектов. [Объект `components`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#componentsObject) может содержать следующее:

- [схемы](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schemaObject);
- [ответы](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#responses-object);
- [параметры](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#parameterObject);
- [примеры](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#parameter-object-examples);
- [тело запроса](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#requestBodyObject);
- [хэдеры](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#headerObject);
- [схемы безопасности](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#securitySchemeObject);
- [ссылки](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#linkObject);
- [коллбэки](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#callbackObject);

Свойства каждого объекта внутри `components` такие же, как и при использовании в других частях спецификации OpenAPI. Используется указатель ссылки (`$ref`), чтобы указать больше деталей в объекте `components`. `$ref` обозначает [объект `reference`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#referenceObject) и является частью JSON.

<a name="reuseParams"></a>
## Переиспользование параметров в нескольких путях

На предыдущем шаге Для параметров мы перечислили все детали непосредственно в объекте `parameters`. Чтобы облегчить переиспользование тех же параметров в других путях, давайте сохраним содержимое `parameters` в `components`. Код ниже показывает, как сделать эти ссылки:

```yaml
paths:
  /weather:
    get:
      tags:
      - Current Weather Data
      summary: "Call current weather data for one location"
      description: "Access current weather data for any location on Earth including over 200,000 cities! Current weather is frequently updated based on global models and data from more than 40,000 weather stations."
      operationId: CurrentWeatherData
      parameters:
        - $ref: '#/components/parameters/q'
        - $ref: '#/components/parameters/id'
        - $ref: '#/components/parameters/lat'
        - $ref: '#/components/parameters/lon'
        - $ref: '#/components/parameters/zip'
        - $ref: '#/components/parameters/units'
        - $ref: '#/components/parameters/lang'
        - $ref: '#/components/parameters/mode'

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

components:

  parameters:
    q:
      name: q
      in: query
      description: "**City name**. *Example: London*. You can call by city name, or by city name and country code. The API responds with a list of results that match a searching word. For the query value, type the city name and optionally the country code divided by a comma; use ISO 3166 country codes."
      schema:
        type: string
    id:
      name: id
      in: query
      description: "**City ID**. *Example: `2172797`*. You can call by city ID. The API responds with the exact result. The List of city IDs can be downloaded [here](http://bulk.openweathermap.org/sample/). You can include multiple cities in this parameter &mdash; just separate them by commas. The limit of locations is 20. *Note: A single ID counts as a one API call. So, if you have city IDs, it's treated as 3 API calls.*"
      schema:
        type: string

    lat:
      name: lat
      in: query
      description: "**Latitude**. *Example: 35*. The latitude coordinate of the location of your interest. Must use with `lon`."
      schema:
        type: string

    lon:
      name: lon
      in: query
      description: "**Longitude**. *Example: 139*. Longitude coordinate of the location of your interest. Must use with `lat`."
      schema:
        type: string

    zip:
      name: zip
      in: query
      description: "**Zip code**. Search by zip code. *Example: 95050,us*. Please note that if the country is not specified, the search uses USA as a default."
      schema:
        type: string

    units:
      name: units
      in: query
      description: '**Units**. *Example: imperial*. Possible values: `standard`, `metric`, and `imperial`. When you do not use the `units` parameter, the format is `standard` by default.'
      schema:
        type: string
        enum: [standard, metric, imperial]
        default: "imperial"

    lang:
      name: lang
      in: query
      description: '**Language**. *Example: en*. You can use lang parameter to get the output in your language. We support the following languages that you can use with the corresponded lang values: Arabic - `ar`, Bulgarian - `bg`, Catalan - `ca`, Czech - `cz`, German - `de`, Greek - `el`, English - `en`, Persian (Farsi) - `fa`, Finnish - `fi`, French - `fr`, Galician - `gl`, Croatian - `hr`, Hungarian - `hu`, Italian - `it`, Japanese - `ja`, Korean - `kr`, Latvian - `la`, Lithuanian - `lt`, Macedonian - `mk`, Dutch - `nl`, Polish - `pl`, Portuguese - `pt`, Romanian - `ro`, Russian - `ru`, Swedish - `se`, Slovak - `sk`, Slovenian - `sl`, Spanish - `es`, Turkish - `tr`, Ukrainian - `ua`, Vietnamese - `vi`, Chinese Simplified - `zh_cn`, Chinese Traditional - `zh_tw`.'
      schema:
        type: string
        enum: [ar, bg, ca, cz, de, el, en, fa, fi, fr, gl, hr, hu, it, ja, kr, la, lt, mk, nl, pl, pt, ro, ru, se, sk, sl, es, tr, ua, vi, zh_cn, zh_tw]
        default: "en"

    mode:
      name: mode
      in: query
      description: "**Mode**. *Example: html*. Determines the format of the response. Possible values are `xml` and `html`. If the mode parameter is empty, the format is `json` by default."
      schema:
        type: string
        enum: [json, xml, html]
        default: "json"
```
Заменим существующий объект `paths` в редакторе Swagger приведенным выше примером кода, включив новый объект `components` и обратим внимание, что отображаемое изображение по-прежнему выглядит так же.              

<a name="reuseObjects"></a>
## Переиспользование объектов `responses`

В [шаге 4: объект `paths`](step4-paths-object.md), когда мы описывали [объект `responses`](step4-paths-object.md#responses) в объекте `paths`, даже с помощью простого заполнителя, мы использовали [объект `schema`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schemaObject) для описания модели запроса или ответа. `schema` относится к структуре данных (поля, значения и иерархия различных объектов и свойств объекта JSON или YAML - см. [Что такое схема?](https://json-schema.org/understanding-json-schema/about.html)).

Давайте поглубже изучим то, как использовать свойства схемы для документирования объекта `response`. Мы также будем хранить  содержимое схемы в `components`, чтобы его можно было повторно использовать в других частях документа спецификации. Если вспомнить [предыдущий шаг](step4-paths-object.md), объект ответов для конечной точки погоды выглядел так:

```yaml
paths:
  /current:
    get:
      parameters:

      ...

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
```

Перенесем описание `schema` для ответа `200` в объект `components`:

```yaml
paths:
  /weather:
    get:
      tags:
      - Current Weather Data
      summary: "Call current weather data for one location"
      description: "Access current weather data for any location on Earth including over 200,000 cities! Current weather is frequently updated based on global models and data from more than 40,000 weather stations."
      operationId: CurrentWeatherData
      parameters:
        - $ref: '#/components/parameters/q'
        - $ref: '#/components/parameters/id'
        - $ref: '#/components/parameters/lat'
        - $ref: '#/components/parameters/lon'
        - $ref: '#/components/parameters/zip'
        - $ref: '#/components/parameters/units'
        - $ref: '#/components/parameters/lang'
        - $ref: '#/components/parameters/mode'

      responses:
        200:
          description: Successful response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/200'
        404:
          description: Not found response
          content:
            text/plain:
              schema:
                title: Weather not found
                type: string
                example: Not found
```

Затем в `components/schemas` мы определим схему `200`.

Прежде чем мы опишем ответ в объекте `components`, может быть полезно посмотреть, как выглядит ответ `weather` от API OpenWeatherMap. Ответ JSON содержит несколько вложенных объектов на разных уровнях.

```json
{
  "coord": {
    "lon": 145.77,
    "lat": -16.92
  },
  "weather": [
    {
      "id": 803,
      "main": "Clouds",
      "description": "broken clouds",
      "icon": "04n"
    }
  ],
  "base": "cmc stations",
  "main": {
    "temp": 293.25,
    "pressure": 1019,
    "humidity": 83,
    "temp_min": 289.82,
    "temp_max": 295.37,
    "sea_level": 984,
    "grnd_level": 990
  },
  "wind": {
    "speed": 5.1,
    "deg": 150
  },
  "clouds": {
    "all": 75
  },
  "rain": {
    "3h": 3
  },
  "snow": {
    "3h": 6
  },
  "dt": 1435658272,
  "sys": {
    "type": 1,
    "id": 8166,
    "message": 0.0166,
    "country": "AU",
    "sunrise": 1435610796,
    "sunset": 1435650870
  },
  "id": 2172797,
  "name": "Cairns",
  "cod": 200
}
```

Существует несколько способов описания этого ответа. Можно создать длинное описание, содержащее всю отраженную иерархию. Однако одной из проблем такого подхода является то, что трудно поддерживать все уровни на одном уровне. С таким количеством вложенных объектов это головокружительно запутанно. Кроме того, легко ошибиться. Хуже всего то, что нельзя переиспользовать отдельные объекты. В первую очередь это подрывает одну из основных причин хранения этого объекта в `components`.    

Другой подход заключается в том, чтобы сделать каждый объект своей сущностью в `components`. Когда объект содержит объект, добавьте значение `$ref`, которое указывает на новый объект. Таким образом, объекты остаются неглубокими (вместо нескольких уровней вложенности), и мы не потеряемся в море запутанных подуровней. (Если подобъекта нет, просто предоставим описание напрямую, без использования `$ref`.

Вот описание ответа `200` для конечной точки `weather`. Я включил тег `paths` для поддержания контекста:

Объект `responses` с документацией `components`:

```yaml
paths:
  /weather:
    get:
      tags:
      - Current Weather Data
      summary: "Call current weather data for one location"
      description: "Access current weather data for any location on Earth including over 200,000 cities! Current weather is frequently updated based on global models and data from more than 40,000 weather stations."
      operationId: CurrentWeatherData
      parameters:
        - $ref: '#/components/parameters/q'
        - $ref: '#/components/parameters/id'
        - $ref: '#/components/parameters/lat'
        - $ref: '#/components/parameters/lon'
        - $ref: '#/components/parameters/zip'
        - $ref: '#/components/parameters/units'
        - $ref: '#/components/parameters/lang'
        - $ref: '#/components/parameters/mode'

      responses:
        200:
          description: Successful response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/200'
        404:
          description: Not found response
          content:
            text/plain:
              schema:
                title: Weather not found
                type: string
                example: Not found

components:

  parameters:
    # not shown for the sake of brevity -- see the earlier code block for details
    ...

  schemas:
    200:
      title: Successful response
      type: object
      properties:
        coord:
          $ref: '#/components/schemas/Coord'
        weather:
          type: array
          items:
            $ref: '#/components/schemas/Weather'
          description: (more info Weather condition codes)
        base:
          type: string
          description: Internal parameter
          example: cmc stations
        main:
          $ref: '#/components/schemas/Main'
        visibility:
          type: integer
          description: Visibility, meter
          example: 16093
        wind:
          $ref: '#/components/schemas/Wind'
        clouds:
          $ref: '#/components/schemas/Clouds'
        rain:
          $ref: '#/components/schemas/Rain'
        snow:
          $ref: '#/components/schemas/Snow'
        dt:
          type: integer
          description: Time of data calculation, unix, UTC
          format: int32
          example: 1435658272
        sys:
          $ref: '#/components/schemas/Sys'
        id:
          type: integer
          description: City ID
          format: int32
          example: 2172797
        name:
          type: string
          example: Cairns
        cod:
          type: integer
          description: Internal parameter
          format: int32
          example: 200
    Coord:
      title: Coord
      type: object
      properties:
        lon:
          type: number
          description: City geo location, longitude
          example: 145.77000000000001
        lat:
          type: number
          description: City geo location, latitude
          example: -16.920000000000002
    Weather:
      title: Weather
      type: object
      properties:
        id:
          type: integer
          description: Weather condition id
          format: int32
          example: 803
        main:
          type: string
          description: Group of weather parameters (Rain, Snow, Extreme etc.)
          example: Clouds
        description:
          type: string
          description: Weather condition within the group
          example: broken clouds
        icon:
          type: string
          description: Weather icon id
          example: 04n
    Main:
      title: Main
      type: object
      properties:
        temp:
          type: number
          description: 'Temperature. Unit Default: Kelvin, Metric: Celsius, Imperial: Fahrenheit.'
          example: 293.25
        pressure:
          type: integer
          description: Atmospheric pressure (on the sea level, if there is no sea_level or grnd_level data), hPa
          format: int32
          example: 1019
        humidity:
          type: integer
          description: Humidity, %
          format: int32
          example: 83
        temp_min:
          type: number
          description: 'Minimum temperature at the moment. This is deviation from current temp that is possible for large cities and megalopolises geographically expanded (use these parameter optionally). Unit Default: Kelvin, Metric: Celsius, Imperial: Fahrenheit.'
          example: 289.81999999999999
        temp_max:
          type: number
          description: 'Maximum temperature at the moment. This is deviation from current temp that is possible for large cities and megalopolises geographically expanded (use these parameter optionally). Unit Default: Kelvin, Metric: Celsius, Imperial: Fahrenheit.'
          example: 295.37
        sea_level:
          type: number
          description: Atmospheric pressure on the sea level, hPa
          example: 984
        grnd_level:
          type: number
          description: Atmospheric pressure on the ground level, hPa
          example: 990
    Wind:
      title: Wind
      type: object
      properties:
        speed:
          type: number
          description: 'Wind speed. Unit Default: meter/sec, Metric: meter/sec, Imperial: miles/hour.'
          example: 5.0999999999999996
        deg:
          type: integer
          description: Wind direction, degrees (meteorological)
          format: int32
          example: 150
    Clouds:
      title: Clouds
      type: object
      properties:
        all:
          type: integer
          description: Cloudiness, %
          format: int32
          example: 75
    Rain:
      title: Rain
      type: object
      properties:
        3h:
          type: integer
          description: Rain volume for the last 3 hours
          format: int32
          example: 3
    Snow:
      title: Snow
      type: object
      properties:
        3h:
          type: number
          description: Snow volume for the last 3 hours
          example: 6
    Sys:
      title: Sys
      type: object
      properties:
        type:
          type: integer
          description: Internal parameter
          format: int32
          example: 1
        id:
          type: integer
          description: Internal parameter
          format: int32
          example: 8166
        message:
          type: number
          description: Internal parameter
          example: 0.0166
        country:
          type: string
          description: Country code (GB, JP etc.)
          example: AU
        sunrise:
          type: integer
          description: Sunrise time, unix, UTC
          format: int32
          example: 1435610796
        sunset:
          type: integer
          description: Sunset time, unix, UTC
          format: int32
          example: 1435650870    
```

Пояснение, как описать ответ будет в следующих разделах. Взглянув на приведенный выше код, стало заметно, что можно использовать не только свойства `$ref` в других частях вашей спецификации, но и внутри `components`.            

> Обратите внимание, как определение схемы включает в себя свойство `example` для каждого элемента? Swagger UI возьмет этот `example` и использует его для динамического построения полного образца кода в секции «Ответы» в выводе пользовательского интерфейса Swagger. Таким образом, не нужны большие куски кода для примеров ответов в нашей спецификации. Вместо этого эти примеры ответов создаются автоматически из схемы. Это одна из приятных вещей в Swagger UI. Таким образом, документация схемы и пример ответа остаются консистентными.

<a name="schema"></a>
## Описание схемы

Для большинства разделов в `components` описаниям объектов тем же, что подробно описаны в остальной части спецификации. При описании объекта `schema` используются стандартные ключевые слова и термины из [схемы JSON](http://json-schema.org/), в частности из [спецификации JSON Schema Wright Draft 00](https://tools.ietf.org/html/draft-wright-json-schema-00).

Другими словами, мы не просто используем термины, определенные в спецификации OpenAPI, для описания моделей вашего JSON. При описании своей модели JSON (структуры данных для входных и выходных объектов), терминология в спецификации OpenAPI вводится в более широкие определения JSON и язык описания для моделирования JSON. Использование OpenAPI схемы JSON является лишь подмножеством полной схемы JSON.

Спецификация OpenAPI не пытается документировать, как моделировать схемы JSON. Это было бы излишним, т.к. уже все задокументировано на сайте [схемы JSON](http://json-schema.org/) и выходило бы за рамки спецификации OpenAPI. Поэтому может понадобиться обратиться к [схеме JSON](http://json-schema.org/) для получения более подробной информации. (Еще одно полезное руководство - [Расширенные данные](http://apihandyman.io/writing-openapi-swagger-specification-tutorial-part-4-advanced-data-modeling/) из API Handyman.)

Для описания JSON объектов можно использовать следующие идентификаторы:

- `title`;
- `multipleOf`;
- `maximum`;
- `exclusiveMaximum`;
- `minimum`;
- `exclusiveMinimum`;
- `maxLength`;
- `minLength`;
- `pattern`;
- `maxItems`;
- `minItems`;
- `uniqueItems`;
- `maxProperties`;
- `minProperties`;
- `required`;
- `enum`;
- `type`;
- `allOf`;
- `oneOf`;
- `anyOf`;
- `not`;
- `items`;
- `properties`;
- `additionalProperties`;
- `description`;
- `format`;
- `default`

Доступные [типы данных](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#data-types):

- `integer`;
- `long`;
- `float`;
- `double`;
- `string`;
- `byte`;
- `binary`;
- `boolean`;
- `date`;
- `dateTime`;
- `password`.

При документировании схемы, лучше начинать с просмотра [объекта `schema`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schemaObject) OpenAPI, а потом, если что-то не покрыто, обратиться к [схеме JSON](https://tools.ietf.org/html/draft-wright-json-schema-00).

Кроме того, посмотрите на некоторые примеры схем. Вы можете посмотреть [примеры 3.0 здесь](https://github.com/OAI/OpenAPI-Specification/tree/master/examples/v3.0). Обычно находят подходящую спецификацию, и имитируют те же свойства и структуру.

> Объект `schema` в версии 3.0 немного отличается от объекта схемы в версии 2.0 - см. [статью о скандинавских API](https://nordicapis.com/whats-new-in-openapi-3-0/#jsonandotherschema) чтобы понять новинки. Тем не менее, примеры схем из  [спецификаций 2.0](https://github.com/OAI/OpenAPI-Specification/tree/master/examples/v2.0) (которые более распространены в сети), также будут полезны, если просто посмотреть на определения схемы, а не на остальную часть спецификации.

<a name="cheat"></a>
## Способ обмануть - автоматически генерировать схему из JSON, используя Stoplight

Описание ответа JSON бывает сложным и запутанным. К счастью, есть несколько простой обходной путь. Можно загрузить [Stoplight](https://next.stoplight.io/) и использовать функцию **Generate JSON**, чтобы Stoplight автоматически создавал описание схемы OpenAPI. Вот ссылка на короткое видео, показывающее, как это сделать:

[![Generate JSON with Stoplight](img/youtube.jpg)](https://youtu.be/0IOWY0Hj3Xc)

По сути, в редактор Stoplight копируется JSON-ответ, который нужно задокументировать. Затем надо нажать `Generate JSON`. Перейти в представление кода и скопировать JSON. Затем сконвертировать JSON в YAML с помощью онлайн-конвертера. Для получения дополнительной информации см. [Stoplight - инструменты визуального моделирования для создания спецификации OpenAPI.](stoplight.md)

Единственная загвоздка в том, что Stoplight использует OpenAPI 2.0, а не 3.0. Возможно, придется использовать API Transformer для преобразования вывода схемы 2.0 в 3.0. Несмотря на это, такой подход может сэкономить много времени.

<a name="gui"></a>
## Использование GUI редакторов для работы с кодом спецификации

На данный момент наверное, есть мысли, насколько будет непрактично и подвержено ошибкам, поскольку работа непосредственно с кодом YAML. По этой причине несколько компаний разработали графические редакторы, чтобы упростить работу с кодом спецификации. В частности, обратите внимание на [Stoplight](stoplight.md), который предоставляет редактор, позволяющий переключаться между кодом и графическим интерфейсом. Smartbear также предлагает [SwaggerHub](swaggerhub-introduction-and-tutorial.md), который не обязательно предоставляет графический интерфейс, но предоставляет встроенные инструменты комментирования и управления версиями.

<a name="appearanse"></a>
## Отображение в Swagger UI

Скопируем код ниже и вставим его в редактор Swagger после объектов `openapi`, `info` и `servers`

```yaml
paths:
  /weather:
    get:
      tags:
      - Current Weather Data
      summary: "Call current weather data for one location"
      description: "Access current weather data for any location on Earth including over 200,000 cities! Current weather is frequently updated based on global models and data from more than 40,000 weather stations."
      operationId: CurrentWeatherData
      parameters:
        - $ref: '#/components/parameters/q'
        - $ref: '#/components/parameters/id'
        - $ref: '#/components/parameters/lat'
        - $ref: '#/components/parameters/lon'
        - $ref: '#/components/parameters/zip'
        - $ref: '#/components/parameters/units'
        - $ref: '#/components/parameters/lang'
        - $ref: '#/components/parameters/mode'

      responses:
        200:
          description: Successful response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/200'
        404:
          description: Not found response
          content:
            text/plain:
              schema:
                title: Weather not found
                type: string
                example: Not found

components:

  parameters:
    q:
      name: q
      in: query
      description: "**City name**. *Example: London*. You can call by city name, or by city name and country code. The API responds with a list of results that match a searching word. For the query value, type the city name and optionally the country code divided by a comma; use ISO 3166 country codes."
      schema:
        type: string
    id:
      name: id
      in: query
      description: "**City ID**. *Example: `2172797`*. You can call by city ID. The API responds with the exact result. The List of city IDs can be downloaded [here](http://bulk.openweathermap.org/sample/). You can include multiple cities in this parameter &mdash; just separate them by commas. The limit of locations is 20. *Note: A single ID counts as a one API call. So, if you have city IDs, it's treated as 3 API calls.*"
      schema:
        type: string

    lat:
      name: lat
      in: query
      description: "**Latitude**. *Example: 35*. The latitude coordinate of the location of your interest. Must use with `lon`."
      schema:
        type: string

    lon:
      name: lon
      in: query
      description: "**Longitude**. *Example: 139*. Longitude coordinate of the location of your interest. Must use with `lat`."
      schema:
        type: string

    zip:
      name: zip
      in: query
      description: "**Zip code**. Search by zip code. *Example: 95050,us*. Please note that if the country is not specified, the search uses USA as a default."
      schema:
        type: string

    units:
      name: units
      in: query
      description: '**Units**. *Example: imperial*. Possible values: `standard`, `metric`, and `imperial`. When you do not use the `units` parameter, the format is `standard` by default.'
      schema:
        type: string
        enum: [standard, metric, imperial]
        default: "imperial"

    lang:
      name: lang
      in: query
      description: '**Language**. *Example: en*. You can use lang parameter to get the output in your language. We support the following languages that you can use with the corresponded lang values: Arabic - `ar`, Bulgarian - `bg`, Catalan - `ca`, Czech - `cz`, German - `de`, Greek - `el`, English - `en`, Persian (Farsi) - `fa`, Finnish - `fi`, French - `fr`, Galician - `gl`, Croatian - `hr`, Hungarian - `hu`, Italian - `it`, Japanese - `ja`, Korean - `kr`, Latvian - `la`, Lithuanian - `lt`, Macedonian - `mk`, Dutch - `nl`, Polish - `pl`, Portuguese - `pt`, Romanian - `ro`, Russian - `ru`, Swedish - `se`, Slovak - `sk`, Slovenian - `sl`, Spanish - `es`, Turkish - `tr`, Ukrainian - `ua`, Vietnamese - `vi`, Chinese Simplified - `zh_cn`, Chinese Traditional - `zh_tw`.'
      schema:
        type: string
        enum: [ar, bg, ca, cz, de, el, en, fa, fi, fr, gl, hr, hu, it, ja, kr, la, lt, mk, nl, pl, pt, ro, ru, se, sk, sl, es, tr, ua, vi, zh_cn, zh_tw]
        default: "en"

    mode:
      name: mode
      in: query
      description: "**Mode**. *Example: html*. Determines the format of the response. Possible values are `xml` and `html`. If the mode parameter is empty, the format is `json` by default."
      schema:
        type: string
        enum: [json, xml, html]
        default: "json"

  schemas:
    200:
      title: Successful response
      type: object
      properties:
        coord:
          $ref: '#/components/schemas/Coord'
        weather:
          type: array
          items:
            $ref: '#/components/schemas/Weather'
          description: (more info Weather condition codes)
        base:
          type: string
          description: Internal parameter
          example: cmc stations
        main:
          $ref: '#/components/schemas/Main'
        visibility:
          type: integer
          description: Visibility, meter
          example: 16093
        wind:
          $ref: '#/components/schemas/Wind'
        clouds:
          $ref: '#/components/schemas/Clouds'
        rain:
          $ref: '#/components/schemas/Rain'
        snow:
          $ref: '#/components/schemas/Snow'
        dt:
          type: integer
          description: Time of data calculation, unix, UTC
          format: int32
          example: 1435658272
        sys:
          $ref: '#/components/schemas/Sys'
        id:
          type: integer
          description: City ID
          format: int32
          example: 2172797
        name:
          type: string
          example: Cairns
        cod:
          type: integer
          description: Internal parameter
          format: int32
          example: 200
    Coord:
      title: Coord
      type: object
      properties:
        lon:
          type: number
          description: City geo location, longitude
          example: 145.77000000000001
        lat:
          type: number
          description: City geo location, latitude
          example: -16.920000000000002
    Weather:
      title: Weather
      type: object
      properties:
        id:
          type: integer
          description: Weather condition id
          format: int32
          example: 803
        main:
          type: string
          description: Group of weather parameters (Rain, Snow, Extreme etc.)
          example: Clouds
        description:
          type: string
          description: Weather condition within the group
          example: broken clouds
        icon:
          type: string
          description: Weather icon id
          example: 04n
    Main:
      title: Main
      type: object
      properties:
        temp:
          type: number
          description: 'Temperature. Unit Default: Kelvin, Metric: Celsius, Imperial: Fahrenheit.'
          example: 293.25
        pressure:
          type: integer
          description: Atmospheric pressure (on the sea level, if there is no sea_level or grnd_level data), hPa
          format: int32
          example: 1019
        humidity:
          type: integer
          description: Humidity, %
          format: int32
          example: 83
        temp_min:
          type: number
          description: 'Minimum temperature at the moment. This is deviation from current temp that is possible for large cities and megalopolises geographically expanded (use these parameter optionally). Unit Default: Kelvin, Metric: Celsius, Imperial: Fahrenheit.'
          example: 289.81999999999999
        temp_max:
          type: number
          description: 'Maximum temperature at the moment. This is deviation from current temp that is possible for large cities and megalopolises geographically expanded (use these parameter optionally). Unit Default: Kelvin, Metric: Celsius, Imperial: Fahrenheit.'
          example: 295.37
        sea_level:
          type: number
          description: Atmospheric pressure on the sea level, hPa
          example: 984
        grnd_level:
          type: number
          description: Atmospheric pressure on the ground level, hPa
          example: 990
    Wind:
      title: Wind
      type: object
      properties:
        speed:
          type: number
          description: 'Wind speed. Unit Default: meter/sec, Metric: meter/sec, Imperial: miles/hour.'
          example: 5.0999999999999996
        deg:
          type: integer
          description: Wind direction, degrees (meteorological)
          format: int32
          example: 150
    Clouds:
      title: Clouds
      type: object
      properties:
        all:
          type: integer
          description: Cloudiness, %
          format: int32
          example: 75
    Rain:
      title: Rain
      type: object
      properties:
        3h:
          type: integer
          description: Rain volume for the last 3 hours
          format: int32
          example: 3
    Snow:
      title: Snow
      type: object
      properties:
        3h:
          type: number
          description: Snow volume for the last 3 hours
          example: 6
    Sys:
      title: Sys
      type: object
      properties:
        type:
          type: integer
          description: Internal parameter
          format: int32
          example: 1
        id:
          type: integer
          description: Internal parameter
          format: int32
          example: 8166
        message:
          type: number
          description: Internal parameter
          example: 0.0166
        country:
          type: string
          description: Country code (GB, JP etc.)
          example: AU
        sunrise:
          type: integer
          description: Sunrise time, unix, UTC
          format: int32
          example: 1435610796
        sunset:
          type: integer
          description: Sunset time, unix, UTC
          format: int32
          example: 1435650870

  securitySchemes:
    app_id:
      type: apiKey
      description: API key to authorize requests. If you don't have an OpenWeatherMap API key, use `fd4698c940c6d1da602a70ac34f0b147`.
      name: appid
      in: query
```

В Swagger UI мы увидим следующее:

![swagger](img/10.png)

> Объект `Responses` объявлен в `components`

В секции  `Responses` просмотрим, как код Example Value был динамически построен из значений `example` в схеме, чтобы показать пример ответа.

А еще, кликнем ссылку **Model** , чтобы увидеть, как описания каждого элемента отображаются в развертываемом / раскладываемом виде:

![Model](img/11.png)

> Отображение описания в Model

<a name="models"></a>
## Раздел Models - почему он существует, как его скрыть

Под всеми эндпоинтами расположен раздел «Модели»:

![downSection](img/12.png)

По умолчанию Swagger UI отображает каждый объект из `components` в разделе «Модели» в конце интерфейса Swagger UI. Если объединить все схемы в один объект, не используя свойство `$ref` для указания на новые объекты, то будет виден только один объект в моделях. Если разделить объекты, то будет виден каждый объект, перечисленный отдельно, включая объект, который содержит все ссылки.

Для переиспользования объектов, определяем каждый объект в `components` отдельно. В результате раздел Модели выглядит как на картинке выше


Почему здесь есть раздел моделей? По-видимому, он был добавлен по популярному запросу, потому что онлайн-редактор Swagger показывал дисплей, и многие пользователи просили включить его в интерфейс Swagger.

Раздел «Модели» не нужен в Swagger UI, поскольку в разделах «Запрос» и «Ответ» пользовательского интерфейса Swagger имеется ссылка «Модель», которая позволяет пользователю переключаться в это представление.

Чтобы скрыть раздел «Модели» можно добавить параметр `defaultModelsExpandDepth: -1` в проект Swagger UI. В этом модуле есть раздел [Руководство Swagger UI](swagger-ui-tutorial.md), в котором подробно описаны параметры Swagger UI, в которых можно настроить этот параметр.

<a name="security"></a>
## Определения `security`

Объект `components` также содержит [объект `securitySchemes`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#securitySchemeObject), который определяет метод авторизации, используемый с каждым путем. Не будем углубляться в детали конфигурации безопасности, исследуем `security` на [шаге 6: объект `security`](step6-security-object.md).


[🔙](step4-paths-object.md)

[Go next ➡](step6-security-object.md)
