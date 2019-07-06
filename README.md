![GitHub repo size in bytes](https://img.shields.io/github/repo-size/docops-hq/learnapidoc-ru.svg)
![GitHub last commit](https://img.shields.io/github/last-commit/docops-hq/learnapidoc-ru.svg?logo=%20)
![GitHub watchers](https://img.shields.io/github/watchers/docops-hq/learnapidoc-ru.svg)
![GitHub stars](https://img.shields.io/github/stars/docops-hq/learnapidoc-ru.svg)

# Курс по документированию REST API

Это вольный перевод курса [**Documenting APIs: A guide for technical writers**](https://idratherbewriting.com/learnapidoc/), составленного Томом Джонсоном, техническим писателем Amazon.

Цель перевода курса:

- пройти курс, научиться документировать API, повысить свои soft skills техписателя;
- освежить знания английского языка;

## Коротко о курсе

Курс по написанию документации REST API предполагает практический подход к документированию REST API вместо лекций об абстрактных понятиях. На этом курсе займемся изучением документации API на примерах использования API сервисов прогноза погоды.

Разбирая API, мы узнаем о конечных точках, параметрах, типах данных, аутентификации, curl, JSON, командной строке, консоли разработчика Chrome, JavaScript и других деталях, связанных с REST API.

Идея курса в следующем: посмотреть на реальные сценарии использования API, вместо изучения концептов API независимо от контекста, что сделает этот курс намного эффективнее.

Во время прохождения курса мы изучим стандарты, инструменты и спецификации REST API. Узнаем о необходимых разделах в документации API, проанализируем примеры документации REST API различных компаний, узнаем, как присоединиться к проекту c открытым исходным кодом, чтобы получить опыт, и многое другое.

# [Начать обучение 👨‍💻](introduction-rest-apis/README.md)

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
    - [**Использование методов с curl**](like-developer/use-methods-with-curl.md)
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
    - [**Практическое занятие: Что не так в разделе API?**](documenting-api-endpoints/whats-wrong.md)
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
    - [**Практическое занятие: Создание спецификации OpenAPI**](openAPI-specification/create-openapi-specification.md)
    - [**Руководство Swagger UI**](openAPI-specification/swagger-ui-tutorial.md)
    - [**Демо Swagger UI**](openAPI-specification/swagger-ui-demo.md)
    - [**Введение и руководство SwaggerHub**](openAPI-specification/swaggerhub-introduction-and-tutorial.md)
    - [**Stoplight - инструмент визуального моделирования для создания спецификаций**](openAPI-specification/stoplight.md)
    - [**Интеграция Swagger с документацией**](openAPI-specification/integrating-swagger-with-docs.md)

5. [**Тестирование документации**](testing-api-doc/README.md)

    - [**Обзор тестирования документации**](testing-api-doc/overview-testing.md)
    - [**Настройка тестовой среды окружения**](testing-api-doc/set-up-test-environment.md)
    - [**Самостоятельное тестирование всех инструкций**](testing-api-doc/test-instructions-yourself.md)
    - [**Тестирование предположений**](testing-api-doc/test-assumptions.md)
    - [**Практическое занятие: Тестирование документации проекта**](testing-api-doc/test-documentation.md)

6. [**Концептуальные разделы**](conceptual-topics/README.md)

    - [**Разделы руководства пользователя**](conceptual-topics/user-guide-topics.md)
    - [**Обзор API**](conceptual-topics/API-overview.md)
    - [**Руководство по началу работы**](conceptual-topics/getting-started.md)
    - [**Требования аутентификации и авторизации**](conceptual-topics/authentication-and-authorization.md)
    - [**Коды статусов и ошибок**](conceptual-topics/status-error-codes.md)
    - [**Ограничения скорости и пределы**](conceptual-topics/rate-limiting.md)
    - [**Описание и образцы кода**](conceptual-topics/code-samples.md)
    - [**SDK и пример приложений**](conceptual-topics/sdks-sample-apps.md)
    - [**Краткое справочное руководство**](conceptual-topics/quick-reference-guide.md)
    - [**API Глоссарий**](conceptual-topics/api-glossary.md)
    - [**Лучшие практики API**](conceptual-topics/best-practices.md)
    - [**Практическое занятие: Оценка концептуального контента в проекте**](conceptual-topics/assess-conceptual-content.md)

7. [**Публикация документации**](Publishing-doc/README.md)

    - [**Обзор вариантов публикации документации**](Publishing-doc/Overview-for-publishing.md)
    - [**Список из 100 сайтов с API документацией**](Publishing-doc/API-doc-sites-list.md)
    - [**Шаблоны проектирования сайтов API документации**](Publishing-doc/Design-patterns.md)
    - [**Инструменты Docs-as-code**](Publishing-doc/Doc-as-code-tools.md)
    - [**Подробнее о Markdown**](Publishing-doc/More-about-Markdown.md)
    - [**Система контроля версий (пример Git)**](Publishing-doc/Version-control-system.md)
    - [**Практическое занятие: Управляем контентом в Wiki Github**](Publishing-doc/Manage-wiki-content.md)
    - [**Практическое занятие: Используем клиент GitHub для десктопа**](Publishing-doc/Use-GitHub-Desctop.md)
    - [**Практическое занятие: процесс Pull request на GitHub**](Publishing-doc/Pull-request-workflows.md)
    - [**Генераторы статичных сайтов**](Publishing-doc/Static-site-generators.md)
    - [**Варианты хостинга и развертывания**](Publishing-doc/Hosting-and-deployment-options.md)
    - [**Возможности автономных CMS**](Publishing-doc/Headless-cms-options.md)
    - [**Рекомендации - какой инструмент документирования выбирать**](Publishing-doc/Which-tool-choose.md)
    - [**Непрерывное развертывание Jekyll и CloudCannon**](Publishing-doc/Jekyll-and-cloudCannon.md)
    - [**Кейс для изучения: Переход на Docs-as-code**](Publishing-doc/Switching-tools.md)

8. [**Работа технического писателя**](Getting-job/README.md)

    - [**Рынок труда технического писателя**](Getting-job/job-market.md)
    - [**Необходимое количество кода, которое нужно знать**](Getting-job/how-much-code-to-know.md)
    - [**Лучшие локации для работы**](Getting-job/best-locations.md)

9. [**Исходные библиотеки API**](Native-library/README.md)

    - [**Обзор нативных библиотек API**](Native-library/Overview-of-library.md)
    - [**Получаем пример Java проекта**](Native-library/Get-the-sample-Java-project.md)
    - [**Java Ускоренный курс**](Native-library/Java-crash-course.md)
    - [**Практическое занятие: Генерация Javadoc из примера проекта**](Native-library/Activity-Generate-Javadoc.md)
    - [**Теги Javadoc**](Native-library/Javadoc-tags.md)
    - [**Изучение вывода Javadoc**](Native-library/Explore-Javadoc-output.md)
    - [**Редактирование тегов Javadoc**](Native-library/Make-edits-Javadocs-tags.md)
    - [**Doxygen, генератор документации для С++**](Native-library/Doxygen.md)
    - [**Создание бессылочной документации при помощи исходных библиотек API**](Native-library/Create-non-refsdocs-with-native-library-APIs.md)

10. [**Глоссарий API и источники**](glossary-and-resourses/README.md)

    - [**Глоссарий API документации**](glossary-and-resourses/Glossary-for-API-documentation.md)
    - [**Практические занятия REST API**](glossary-and-resourses/RESTAPI-activities.md)
    - [**Практическое занятие: Получить информацию о событии, используя API сервиса Eventbrite**](glossary-and-resourses/Get-event-information-using-Eventbrite-API.md)
    - [**Практическое занятие: Извлечь галерею, используя API сервиса Flikr**](glossary-and-resourses/Retrieve-gallery-using-Flickr-API.md)
    - [**Получить скорость ветра, используя API сервиса Aeris Weather**](glossary-and-resourses/Get-wind-speed-using-Aeris-API.md)
    - [**Справочник RAML**](glossary-and-resourses/RAML-tutorial.md)
    - [**Справочник API Blueprint**](glossary-and-resourses/API-Blueprint-tutorial.md)
    - [**Описание ошибок**](glossary-and-resourses/answeres-whats-wrong.md)

11. [**Документирование кода**](doc-code/doc-code.md)

# [Go next ➡](introduction-rest-apis/README.md)
