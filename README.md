![GitHub repo size in bytes](https://img.shields.io/github/repo-size/Starkovden/Documenting_APIs.svg?style=plastic)
![GitHub last commit](https://img.shields.io/github/last-commit/Starkovden/Documenting_APIs.svg?logo=%20)
![GitHub watchers](https://img.shields.io/github/watchers/Starkovden/Documenting_APIs.svg?style=social)
![GitHub stars](https://img.shields.io/github/stars/Starkovden/Documenting_APIs.svg?style=social)

# Курс по созданию API документации

Материалы, размещенные в данном репозитории являются вольным переводом курса [**Documenting APIs: A guide for technical writers**](https://idratherbewriting.com/learnapidoc/)  составленного Томом Джонсоном, техническим писателем Amazon.

Перевод курса по мере возможностей.

Цель перевода курса:

- пройти курс, научиться документировать API, повысить свои soft skills техписателя;
- освежить знания английского языка;

## Вкратце о курсе

Курс по написанию документации REST API предполагает практический подход к документированию REST API вместо простых разговорах об абстрактных понятиях. Изучим документацию API на примерах использования API сервисов прогноза погоды.

Разбирая API, узнаем о конечных точках, параметрах, типах данных, аутентификации, curl, JSON, командной строке, консоли разработчика Chrome, JavaScript и других деталях, связанных с REST API.

Идея курса: погружение в реальные сценарии использования API, вместо изучения концепций API независимо от контекста, что делает этот курс намного эффективнее.

Во время прохождения курса изучим стандарты, инструменты и спецификации REST API. Узнаем о необходимых разделах в документации API, проанализируем примеры документации REST API различных компаний, узнаем, как присоединиться к опен-сорс проекту, чтобы получить опыт, и многое другое.

## Модули курса

1. [**Введение в REST API**](introduction-rest-apis/README.md)

    - [**Обзор курса**](introduction-rest-apis/course-overview.md)

    - [**Видео презентации**](introduction-rest-apis/video-presentations.md)

    - [**Слайды курса**](introduction-rest-apis/course-slides.md)

    - [**Практические занятия**](introduction-rest-apis/workshop-activities.md)

    - [**Для чего этот курс**](introduction-rest-apis/what-for-this-course.md)

    - [**Об авторе**](introduction-rest-apis/about-the-author.md)

    - [**Рынок документации REST API**](introduction-rest-apis/api-doc-market.md)

    - [**Что такое REST API**](introduction-rest-apis/what-is-rest-api.md)

    - [**Практика: Определение цели**](introduction-rest-apis/identify-goals.md)

2. [**Использование API в роли разработчика**](like-developer/README.md)

    - [**Сценарий использования API погоды**](like-developer/using-api-scenario.md)

    - [**Получение ключей авторизации**](like-developer/get-authorization-keys.md)

    - [**Отправка запросов в Postman**](like-developer/submit-requests-postman.md)

    - [**Введение и установка curl**](like-developer/curl-intro-and-instalation.md)

    - [**Создание curl запроса**](like-developer/make-curl-call.md)

    - [**Понимание curl**](like-developer/understand-curl.md)

    - [**Использование методов с curl**](use-methods-with-curl.md)

    - [**Анализ JSON ответов**](like-developer/analyze-json-response.md)

    - [**Изучение полезных данных JSON ответа**](like-developer/inspect-json.md)

    - [**Доступ и вывод на страницу определенного значения JSON**](like-developer/access-print-value.md)

    - [**Погружение в точечную нотацию**](like-developer/dot-notation.md)

3. [**Документирование конечных точек**](documenting-api-endpoints/README.md)

    - [**Документирование новой конечной точки**](documenting-api-endpoints/new-endpoint.md)

    - [**Обзор пошагового описания API ссылки**](documenting-api-endpoints/api-reference-tutorial-overview.md)

    - [**Шаг 1: Описание ресурса**](documenting-api-endpoints/step1-resourse-description.md)

    - [**Шаг 2: Конечные точки и методы**](documenting-api-endpoints/step2-endpoints-and-methods.md)

    - [**Шаг 3: Параметры**](documenting-api-endpoints/step3-parameters.md)

    - [**Шаг 4: Пример запроса**](documenting-api-endpoints/step4-request-example.md)

    - [**Шаг 5: Пример и схема ответа**](documenting-api-endpoints/step5-response-example-and-schema.md)

    - [**Собираем все вместе**](documenting-api-endpoints/putt-all-together.md)

    - [**Практическое занятие: Поиск open-source проекта**](documenting-api-endpoints/find-open-source-project.md)

    - [**Практическое занятие: Оценка ключевых элементов API документации**](documenting-api-endpoints/evaluate-api-referense-docs.md)

4. [**Спецификация OpenAPI и Swagger**](openAPI-specification/README.md)

    - [**Обзор форматов спецификаций REST API**](openAPI-specification/overview-specification-formats.md)

    - [**Знакомство со спецификациями OpenAPI и Swagger**](openAPI-specification/introduction-openapi-and-swagger.md)

    - [**Работа в YAML**](openAPI-specification/working-in-YAML.md)

    - [**Обзор руководства OpenAPI**](openAPI-specification/openapi-tutorial-overview.md)

    - [**Шаг 1: Объект `openapi`**](openAPI-specification/step1-openapi-object.md)

    - [**Шаг 2: Объект `info`**](openAPI-specification/step2-info-object.md)

    - [**Шаг3: Объект `servers`**](openAPI-specification/step3-servers-object.md)

    - [**Шаг 4: Объект `paths`**](openAPI-specification/step4-paths-object.md)

    - [**Шаг 5: Объект `components`**](openAPI-specification/step5-components-object.md)

    - [**Шаг 6: Объект `security`**](openAPI-specification/step6-security-object.md)

    - [**Шаг 7: Объект `tags`**](openAPI-specification/step7-tags-object.md)

    - [**Шаг 8: Объект `externalDocs`**](openAPI-specification/step8-externalDocs-object.md)

    - [**Практическое занятие: Создание спецификации OpenAPI**](openAPI-specification/сreate-openapi-specification.md)

    - [**Руководство Swagger UI**](openAPI-specification/swagger-ui-tutorial.md)

    - [**Демо Swagger UI**](openAPI-specification/swagger-ui-demo.md)

    - [**Введение и руководство SwaggerHub**](openAPI-specification/swaggerhub-introduction-and-tutorial.md)

    - [**Stoplight - инструмент визуального моделирования для создания спецификаций**](openAPI-specification/stoplight.md)

    - [**Интеграция Swagger с документацией**](openAPI-specification/integrating-swagger-with-docs.md)

5. [**Тестирование документации**](testing-api-doc/README.md)

    - [**Обзор тестирования документации**](overview-testing.md)

    - [**Настройка тестовой среды окружения**](set-up-test-environment.md)

    - [**Самостоятельное тестирование всех инструкций**](test-instructions-yourself.md)

    - [**Тестирование предположений**](test-assumptions.md)

    - [**Практическое занятие: Тестирование документации проекта**](test-documentation.md)

6. [**Концептуальные разделы**](conceptual-topics/README.md)
7. [**Публикация документации**](Publishing-doc/README.md)
8. [**Работа технического писателя**](Getting-job/README.md)
9. [**Исходные библиотеки API**](Native-library/README.md)
10. [**Глоссарий API и источники**](glossary-and-resourses/README.md)
