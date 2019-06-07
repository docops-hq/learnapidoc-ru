# Справочник API Blueprint

API Blueprint, так же, как и Swagger определяет спецификацию для описания REST API. Инструменты, которые поддерживают API Blueprint, могут читать и отображать информацию.

> Если не используется платформа, которая требует именно  API Blueprint, лучше использовать [спецификацию OpenAPI](../openAPI-specification/openapi-tutorial-overview.md).

[Что такое API Blueprint](#apiblueprint)

[Пример blueprint](#sample)

[Анализ blueprint](#parsing)

[Создаем пример вывода HTML используя API Blueprint и Apiary](#createSample)

- [Создаем проект Apiary](#project)
- [Взаимодействие с API на Apiary](#interact)

<a name="apiblueprint"></a>
## Что такое API Blueprint

Спецификация API Blueprint написана с использованием синтаксиса Markdown. Blueprint представляет собой конкретную схему, которая является допустимой или недействительной на основе имен элементов, порядка, расстояния и других деталей. Поэтому, он не так гибок, как Markdown. Но он может быть предпочтительнее, чем YAML.

<a name="sample"></a>
## Пример blueprint

Вот пример Blueprint для понимания синтаксиса:

```markdown
FORMAT: 1A
HOST: http://polls.apiblueprint.org/

# test

Polls is a simple API allowing consumers to view polls and vote in them.

# Polls API Root [/]

This resource does not have any attributes. Instead, it offers the initial
API affordances in the form of the links in the JSON body.

It is recommended to follow the “url" link values,
[Link](https://tools.ietf.org/html/rfc5988), or Location headers where
applicable to retrieve resources. Instead of constructing your own URLs,
to keep your client decoupled from implementation details.

## Retrieve the Entry Point [GET]

+ Response 200 (application/json)

        {
            "questions_url": "/questions"
        }

## Group Question

Resources related to questions in the API.

## Question [/questions/{question_id}]

A Question object has the following attributes:

+ question
+ published_at - An ISO8601 date when the question was published.
+ url
+ choices - An array of Choice objects.

+ Parameters
    + question_id: 1 (required, number) - ID of the Question in form of an integer

### View a Questions Detail [GET]

+ Response 200 (application/json)

        {
            "question": "Favourite programming language?",
            "published_at": "2014-11-11T08:40:51.620Z",
            "url": "/questions/1",
            "choices": [
                {
                    "choice": "Swift",
                    "url": "/questions/1/choices/1",
                    "votes": 2048
                }, {
                    "choice": "Python",
                    "url": "/questions/1/choices/2",
                    "votes": 1024
                }, {
                    "choice": "Objective-C",
                    "url": "/questions/1/choices/3",
                    "votes": 512
                }, {
                    "choice": "Ruby",
                    "url": "/questions/1/choices/4",
                    "votes": 256
                }
            ]
        }

## Choice [/questions/{question_id}/choices/{choice_id}]

+ Parameters
    + question_id: 1 (required, number) - ID of the Question in form of an integer
    + choice_id: 1 (required, number) - ID of the Choice in form of an integer

### Vote on a Choice [POST]

This action allows you to vote on a question's choice.

+ Response 201

    + Headers

            Location: /questions/1

## Questions Collection [/questions{?page}]

+ Parameters
    + page: 1 (optional, number) - The page of questions to return

### List All Questions [GET]

+ Response 200 (application/json)

    + Headers

            Link: </questions?page=2>; rel="next"

    + Body

            [
                {
                    "question": "Favourite programming language?",
                    "published_at": "2014-11-11T08:40:51.620Z",
                    "url": "/questions/1",
                    "choices": [
                        {
                            "choice": "Swift",
                            "url": "/questions/1/choices/1",
                            "votes": 2048
                        }, {
                            "choice": "Python",
                            "url": "/questions/1/choices/2",
                            "votes": 1024
                        }, {
                            "choice": "Objective-C",
                            "url": "/questions/1/choices/3",
                            "votes": 512
                        }, {
                            "choice": "Ruby",
                            "url": "/questions/1/choices/4",
                            "votes": 256
                        }
                    ]
                }
            ]

### Create a New Question [POST]

You may create your own question using this action. It takes a JSON
object containing a question and a collection of answers in the
form of choices.

+ question (string) - The question
+ choices (array[string]) - A collection of choices.

+ Request (application/json)

        {
            "question": "Favourite programming language?",
            "choices": [
                "Swift",
                "Python",
                "Objective-C",
                "Ruby"
            ]
        }

+ Response 201 (application/json)

    + Headers

            Location: /questions/2

    + Body

            {
                "question": "Favourite programming language?",
                "published_at": "2014-11-11T08:40:51.620Z",
                "url": "/questions/2",
                "choices": [
                    {
                        "choice": "Swift",
                        "url": "/questions/2/choices/1",
                        "votes": 0
                    }, {
                        "choice": "Python",
                        "url": "/questions/2/choices/2",
                        "votes": 0
                    }, {
                        "choice": "Objective-C",
                        "url": "/questions/2/choices/3",
                        "votes": 0
                    }, {
                        "choice": "Ruby",
                        "url": "/questions/2/choices/4",
                        "votes": 0
                    }
                ]
            }
```

Справочники по синтакису API Blueprint можно посмотреть на ресурсах:

- [API Blueprint tutorial](https://apiblueprint.org/documentation/tutorial.html)
- [Apiary tutorial](https://help.apiary.io/api_101/api_blueprint_tutorial/)
- [Github API Blueprint tutorial](https://github.com/apiaryio/api-blueprint/blob/master/Tutorial.md)

Различные примеры Blueprint можно посмотреть [здесь](https://github.com/apiaryio/api-blueprint/tree/master/examples) Примеры помогают понять различные аспекты спецификации.

<a name="parsing"></a>
## Анализ blueprint

<a name="createSample"></a>
## Создаем пример вывода HTML используя API Blueprint и Apiary

<a name="project"></a>
### Создаем проект Apiary

<a name="interact"></a>
### Взаимодействие с API на Apiary






















[🔙](RAML-tutorial.md)

[Go next ➡](what's-wrong.md)
