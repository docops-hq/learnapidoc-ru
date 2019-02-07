# Обзор форматов спецификаций REST API

При [представлении REST API](https://github.com/Starkovden/Documenting_APIs/blob/master/1.%20Introduction%20to%20REST%20APIs/1.8.What%20is%20REST%20API.md), было упомянуто, что REST API следуют архитектурному стилю, а не конкретному стандарту. Тем не менее, было разработано несколько спецификаций REST, чтобы попытаться представить стандарты в виде описания API REST. Вот три наиболее популярных спецификации REST API: [OpenAPI (формально называется Swagger)](https://github.com/OAI/OpenAPI-Specification), [RAML](https://raml.org/) и [API Blueprint](https://apiblueprint.org/).

В первые годы спецификаций между форматами существовала здоровая конкуренция. Но теперь, без сомнения, спецификация OpenAPI является самой популярной, с наибольшим сообществом, динамикой и различными инструментами. Из-за этого больше всего времени уделено OpenAPI в этом курсе. Фактически весь этот модуль посвящен спецификации OpenAPI. ([RAML](https://github.com/Starkovden/Documenting_APIs/blob/master/10.%20API%20glossary%20and%20Resourses/10.6.%20RAML%20tutorial.md) и [API Blueprint](https://github.com/Starkovden/Documenting_APIs/blob/master/10.%20API%20glossary%20and%20Resourses/10.7.%20API%20Blueprint%20tutorial.md) размещены в модуле [Глоссарий API и источники](https://github.com/Starkovden/Documenting_APIs/tree/master/10.%20API%20glossary%20and%20Resourses) в конце курса.)

> «OpenAPI» относится к спецификации, а «Swagger» относится к инструментам API, которые считывают и отображают информацию в спецификации. Подробный рассказ об OpenAPI и Swagger в следующих разделах.

В целом, спецификации REST API приводят к улучшению структуры документации. Помните, что эти спецификации REST API в основном описывают эталонные [конечные точки в API](https://github.com/Starkovden/Documenting_APIs/tree/master/3.%20Documenting%20API%20endpoints). Хотя эти разделы важны, помимо них необходима еще и иная документации. (Вот почему создан отдельный модуль [Безадресные разделы API](https://github.com/Starkovden/Documenting_APIs/tree/master/6.%20Non-reference%20API%20topics).)

Тем не менее, документация, которую покрывает спецификация, часто составляет основную ценность API, поскольку она касается конечных точек и их ответов.

Запись в спецификации вводит новое измерение в документацию, которое делает документацию API по существу уникальной. Овладев форматом спецификации OpenAPI, мы сможем значительно отличаться от других технических писателей.
