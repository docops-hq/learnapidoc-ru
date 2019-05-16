# Введение в curl и его установка


Хотя Postman удобен, его трудно использовать для представления в документации, как совершать звонки с его помощью. Кроме того, разные пользователи, вероятно, используют разные клиенты с графическим интерфейсом или вообще не используют их (предпочитая командную строку)

Вместо того, чтобы описывать, как выполнять вызовы REST с использованием GUI-клиента, такого как Postman, наиболее традиционный метод документирования синтаксиса запроса - использовать curl.

[О curl](#about)

[Установка curl](#instalCurl)

[Установка на MacOS](#macInstall)

[Установка на Windows](#winInstall)

[Создание тестового вызова API](#testCall)

[curl и Windows](#curlvsWindows)

<a name="about"></a>
## О curl

curl - это утилита командной строки, которая позволяет выполнять HTTP-запросы с различными параметрами и методами. Вместо того, чтобы переходить к веб-ресурсам в адресной строке браузера, можно использовать командную строку, чтобы получить те же ресурсы, извлеченные в виде текста.

> Иногда curl пишется как cURL, что означает Client URL. "curl" является более распространенным написанием, так что оба варианта верны.

<a name="instalCurl"></a>
## Установка curl

curl доступен на MacOS по умолчанию, для Windows требуется установка. Ниже представлены инструкции по установке curl.

<a name="macInstall"></a>
### Установка на MacOS

Проверить установлен ли curl на MacOS можно так:

1. Открываем Терминал (нажимаем `Cmd`+`spacebar` для открытия Спотлайт и вводим *Terminal*).
2. В терминале пишем `curl -V`. Ответ должен быть примерно таким:

```
curl 7.54.0 (x86_64-apple-darwin16.0) libcurl/7.54.0 SecureTransport zlib/1.2.8
Protocols: dict file ftp ftps gopher http https imap imaps ldap ldaps pop3 pop3s rtsp smb smbs smtp smtps telnet tftp Features: AsynchDNS IPv6 Largefile GSS-API Kerberos SPNEGO NTLM NTLM_WB SSL libz UnixSockets
```

Если такого ответа нет, то curl необходимо [скачать и установить](https://curl.haxx.se/)

<a name="winInstall"></a>
### Установка на Windows

Установка curl в Windows включает другие шаги. Сначала определяем версию windows:  32-разрядная или 64-разрядная версия Windows, щелкнув правой кнопкой мыши `Компьютер` и выбрав `Свойства`. Затем следуем [инструкциям на этой странице](http://www.confusedbycode.com/curl/#downloads). Нужно выбрать одну из бесплатных версий с правами Администратора.

После установки проверяем версию установленной curl;

1. Открываем командную строку нажав кнопку `Пуск` и введя `cmd`
2. В строке пишем `curl -V`

Ответ должен быть примерно таким:

```
curl 7.54.0 (x86_64-apple-darwin14.0) libcurl/7.37.1 SecureTransport zlib/1.2.5
Protocols: dict file ftp ftps gopher http https imap imaps ldap ldaps pop3 pop3s rtsp smtp smtps telnet tftp
Features: AsynchDNS GSS-Negotiate IPv6 Largefile NTLM NTLM_WB SSL libz
```

<a name="testCall"></a>
## Создание тестового вызова API

После установки curl делаем тестовый вызов API

```javascript
curl -X GET "https://api.openweathermap.org/data/2.5/weather?zip=95050&appid=fd4698c940c6d1da602a70ac34f0b147&units=imperial"
```

В ответ должен вернуться мнимизированный JSON:

```yaml
{"coord":{"lon":-121.96,"lat":37.35},"weather":[{"id":701,"main":"Mist","description":"mist","icon":"50d"}],"base":"stations","main":{"temp":66.92,"pressure":1017,"humidity":50,"temp_min":53.6,"temp_max":75.2},"visibility":16093,"wind":{"speed":10.29,"deg":300},"clouds":{"all":75},"dt":1522526400,"sys":{"type":1,"id":479,"message":0.0051,"country":"US","sunrise":1522504404,"sunset":1522549829},"id":420006397,"name":"Santa Clara","cod":200}
```

> В Windows в командной строке не работает `Ctrl+V`, нужно нажать правой кнопкой мыши и выбрать `paste`.

<a name="curlvsWindows"></a>
## curl и Windows

Если вы используете Windows, обратите внимание на следующие требования к форматированию при использовании curl:

- Используйте двойные кавычки в командной строке Windows. (Windows не поддерживает одинарные кавычки.);
- Не используйте обратную косую черту (\) для разделения строк. (Это только для удобства чтения и не влияет на вызов на Mac.)
- Добавив -k в команду curl, вы можете обойти сертификат безопасности curl, который может быть необходимым.
