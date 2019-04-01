# Руководство OpenAPI Шаг 6: Объект `security` 

| [*Шаг 1: объект* `openapi`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.5.%20Step%201%20The%20openapi%20object.md) | --> | [*Шаг 2: объект* `info`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.6.%20Step%202%20The%20info%20object.md) | --> | [*Шаг 3: объект* `servers`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.7.%20Step%203%20The%20servers%20object.md) | --> | [*Шаг 4: объект* `paths`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.8.%20Step%204%20The%20paths%20object.md) | --> | [*Шаг 5: объект* `components`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.9.%20Step%205%20The%20components%20object.md) | --> | [**Шаг 6: объект** `security`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.10.%20Step%206%20security%20object.md) | --> | [*Шаг 7: объект* `tags`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.11.%20Step%207%20The%20tags%20object.md) | --> | [*Шаг 8: объект* `externalDocs`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.12.%20Step%208%20The%20externalDocs%20object.md) |

Swagger UI предоставляет функцию **Try it out**, которая позволяет пользователям отправлять реальные запросы. Для отправки запросов, авторизованных нашим сервером API, спецификация должна содержать информацию о безопасности, которая авторизует запрос. [Объект `security`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#securityRequirementObject) указывает протокол безопасности или авторизации, используемый при отправке запросов.

[Выбор схемы безопасности](#which)

[Авторизация API ключом](#apikeyAuth)

[Объект `security`](#securityObject)

[Ссылка на схему безопасности в компонентах](#schmenaInComponents)

[Отображение в Swagger UI](#appearanse)

[Тест авторизации](#test)

<a name="which"></a>
## Выбор схемы безопасности

В API REST могут использоваться различные подходы безопасности для авторизации запросов. Рассмотрим наиболее распространенные методы авторизации в [Требованиях аутентификации и авторизации](https://github.com/Starkovden/Documenting_APIs/blob/master/6.%20Non-reference%20API%20topics/6.4.%20Authentification%20and%20authorization.md). Swagger UI поддерживает четыре схемы авторизации:

- API ключ;
- HTTP;
- OAuth 2.0;
- Open ID Connect.

На этом шаге руководства по OpenAPI мы будем использовать подход с использованием API ключа, поскольку именно его использует API-интерфейс OpenWeatherMap. Если ваш API использует [OAuth 2.0]() или другой метод, надо прочитать [Security Scheme information](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#security-scheme-object), чтобы узнать, как ее настроить. Тем не менее, все методы безопасности в основном следуют одному и тому же шаблону.

<a name="apikeyAuth"></a>
## Авторизация API ключом

В примере API OpenWeatherMap, который мы используем в этом курсе, используется ключ API, переданный в строке запроса URL-адреса (а не в заголовке). Если вы отправляете запрос без ключа API в строке запроса (или без действительного ключа API), сервер отклоняет запрос. Для получения подробной информации о модели авторизации OpenWeatherMap см. [How to start](https://openweathermap.org/appid#use).

<a name="securityObject"></a>
## Объект `security`

На корневом уровне документа OpenAPI добавим объект `security`, который определяет глобальный метод безопасности API:

    security:
    - app_id: []

`app_id` - произвольное имя, которое мы дали этой схеме безопасности в нашем объекте `securitySchemes`. Мы могли бы назвать ее как угодно. Мы определим `app_id` в `components`.

Все пути будут использовать метод безопасности `app_id` по умолчанию, если он не переопределен значением на [уровне объекта `path`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.8.%20Step%204%20The%20paths%20object.md). Например, на уровне пути мы могли бы перезаписать метод глобальной безопасности следующим образом:

    /current:
      get:
        ...
        security:
        - some_other_key: []


Тогда путь `weather` будет использовать метод безопасности `some_other_key`, в то время как все другие пути будут использовать глобально объявленную безопасность `app_id`.

<a name="schmenaInComponents"></a>
## Ссылка на схему безопасности в компонентах

В [объекте `components`](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/4.9.%20Step%205%20The%20components%20object.md) добавим [объект `securitySchemes`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#securitySchemeObject), который определяет подробности о схеме безопасности, которую использует API:

    components:
      ...

      securitySchemes:
        app_id:
          type: apiKey
          description: API key to authorize requests. If you don't have an OpenWeatherMap API key, use `fd4698c940c6d1da602a70ac34f0b147`.
          name: appid
          in: query

Свойства, которые можно использовать для каждого элемента в объекте `securitySchemes`, включают следующее:

- `type`: протокол авторизации - `apiKey`, `http`, `oath2` или `openIdConnect`.
- `description`: Описание метода безопасности. В Swagger UI это описание появляется в модале авторизации (см. Скриншот ниже). CommonMark Markdown разрешена.
- `name`: Имя значения заголовка, представленного в запросе. Используется только для безопасности типа `apiKey`.
- `in`: Указывает, где применяется ключ безопасности. Варианты: `query`, `header` или `cookie`. Используется только для безопасности типа `apiKey`.
- `scheme`: Используется с авторизацией типа `http`.
- `bearerFormat`: Используется с авторизацией типа `http`.
- [объект `flow`](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#oauthFlowsObject): Используется с авторизацией типа `oath2`
- `openIdConnectUrl`: Используется с авторизацией типа `openIdConnect`

<a name="appearanse"></a>
## Отображение в Swagger UI

В редакторе Swagger, если еще не указано, добавим объект `security` на корневом уровне:

    security:
    - app_id: []

И вставим объект `securitySchemes` в объект `components` (на том же уровне, что и `parameters` и `responses`):

    components:
      parameters:
      ...
      responses:
      ...

      securitySchemes:
        app_id:
          type: apiKey
          description: API key to authorize requests. If you don't have an OpenWeatherMap API key, use `fd4698c940c6d1da602a70ac34f0b147`.
          name: appid
          in: query

И проверим, как изменился наш Swagger UI в правой части: появилась кнопка `Authorize`

![Authorize](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/img/13.png?raw=true)

>Добавление в спецификацию информации о безопасности

Если нажать на кнопку, то появится `description` и другие детали авторизации:

![button](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/img/14.png?raw=true)

После ввода ключа API ([Ключ мы получали во втором модуле](https://github.com/Starkovden/Documenting_APIs/blob/master/2.%20Using%20an%20API%20like%20a%20developer/2.2.Get%20authorization%20keys.md#-%D0%BF%D1%80%D0%B0%D0%BA%D1%82%D0%B8%D0%BA%D0%B0-%D0%BF%D0%BE%D0%BB%D1%83%D1%87%D0%B0%D0%B5%D0%BC-%D0%BA%D0%BB%D1%8E%D1%87-%D0%B0%D0%B2%D1%82%D0%BE%D1%80%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D0%B8-openweathermap-api)) и нажатия кнопки `Authorize` метод авторизации устанавливается для любого количества запросов. Сессия авторизации истекает только тогда, когда пользователи обновляют страницу.

<a name="test"></a>
## Тест авторизации

Теперь, когда мы добавили авторизацию, попробуем сделать фактический запрос API. В редакторе Swagger (правая панель) нажмите кнопку `Authorize`, вставляем образец ключа API, показанного в описании, в поле **Value** (или используйте свой собственный ключ API OpenWeatherMap) и нажимаем `Authorize`. После чего кликаем `Close` , чтобы закрыть окно авторизации.

В разделе «Current Weather Data» разворачиваем конечную точку погоды GET и кликаем `Try it out`. В поле почтовый индекс введем свой почтовый индекс и сокращение страны (например, 95050, США), а затем нажмите `Execute`.

При выполнении запроса, Swagger UI показывает отправленный запрос. Например, после выполнения запроса погоды, curl выглядит следующим образом:

    curl -X GET "https://api.openweathermap.org/data/2.5/weather?zip=95050%2Cus&units=imperial&lang=en&mode=json&appid=fd4698c940c6d1da602a70ac34f0b147" -H "accept: application/json"


`&Appid = fd4698c940c6d1da602a70ac34f0b147` "указывает, что ключ API включается в строку запроса, поэтому запрос будет авторизован. Если вы скопируете отправленный curl и вставите его в командную строку, вы увидите успешный ответ:

![response](https://github.com/Starkovden/Documenting_APIs/blob/master/4.%20OpenAPI%20specification%20and%20Swagger/img/15.png?raw=true)

> Успешный curl response

Ответ сервера также отображается непосредственно в Swagger UI со ссылкой для его загрузки:

    {
      "coord": {
        "lon": -121.96,
        "lat": 37.35
      },
      "weather": [
        {
          "id": 500,
          "main": "Rain",
          "description": "light rain",
          "icon": "10d"
        },
        {
          "id": 701,
          "main": "Mist",
          "description": "mist",
          "icon": "50d"
        }
      ],
      "base": "stations",
      "main": {
        "temp": 55.24,
        "pressure": 1012,
        "humidity": 77,
        "temp_min": 51.08,
        "temp_max": 59
      },
      "visibility": 16093,
      "wind": {
        "speed": 5.82,
        "deg": 320
      },
      "rain": {
        "1h": 0.25
      },
      "clouds": {
        "all": 40
      },
      "dt": 1544039760,
      "sys": {
        "type": 1,
        "id": 5122,
        "message": 0.0052,
        "country": "US",
        "sunrise": 1544022470,
        "sunset": 1544057391
      },
      "id": 420006397,
      "name": "Santa Clara",
      "cod": 200
    }


Обратите внимание, если вы обнаружите при реализации Swagger UI, что запрос curl работает? но ответ не отображается в Swagger UI, может возникнуть проблема CORS с вашими запросами на блокировку API от веб-приложений, таких как Swagger. Подробнее см. [Troubleshooting issues with Swagger UI]().
