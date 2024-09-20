[![CI](https://github.com//ai-forever/gigachain/actions/workflows/check_diffs.yml/badge.svg)](https://github.com//ai-forever/gigachain/actions/workflows/check_diffs.yml)
[![Downloads](https://static.pepy.tech/badge/gigachain/month)](https://pepy.tech/project/gigachain)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

<br />
<div align="center">

  <a href="https://github.com/ai-forever/gigachain">
    <img src="docs/static/img/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h1 align="center">🦜️🔗 GigaChain (GigaChat + LangChain)</h1>

  <p align="center">
    Библиотека для разработки LangChain-style приложений на русском языке с поддержкой GigaChat
    <br />
    <a href="https://github.com/ai-forever/gigachain/issues">Создать issue</a>
    ·
    <a href="https://developers.sber.ru/docs/ru/gigachat/sdk/overview">Документация GigaChain</a>
  </p>
</div>


![Product Name Screen Shot](/docs/static/img/logo-with-backgroung.png)

## 🤔 О GigaChain

GigaChain – это фреймворк для разработки приложений с использованием больших языковых моделей (LLM).
GigaChain является ответвлением open source проекта [LangChain](https://github.com/langchain-ai/langchain).

Отличительная особенность GigaChain — ориентация на создание русскоязычных решений и умение работать с такими нейросетями, как [GigaChat](https://giga.chat/). При этом фреймворк полностью совместим со всеми популярными моделями и компонентами LangChain.

GigaChain значительно упрощает решение задач, требующих использования больших языковых моделей (**LLM**). Например, таких, как генерация на основе собственных источников (*RAG*), создание мультиагентных систем, суммаризация данных, и других.

За работу с GigaChat отвечает [одноименный модуль](https://github.com/ai-forever/gigachat), который автоматически формирует запросы в соответствии с форматом [GigaChat API](https://developers.sber.ru/docs/ru/gigachat/api/overview) и передает их в выбранную [модель](https://developers.sber.ru/docs/ru/gigachat/models).

Подробное описание архитектуры и компонентов GigaChain — в [официальной документации](https://developers.sber.ru/docs/ru/gigachain/concepts/overview).

## Быстрый старт

Для начала работы с GigaChain посмотрите короткое видео или следуйте инструкциям ниже.

[![GigaChain быстрый старт](https://img.youtube.com/vi/HAg-GFKl1rc/maxresdefault.jpg)](https://www.youtube.com/watch?v=HAg-GFKl1rc)

Установите GigaChain:

```sh
pip install gigachain-community
```

Запустите простой пример:

```py
from langchain_core.messages import HumanMessage, SystemMessage
from langchain_community.chat_models.gigachat import GigaChat

# Авторизация в GigaChat
llm = GigaChat(
    credentials="<авторизационные_данные>",
    scope="GIGACHAT_API_PERS",
    model="GigaChat",
    # Отключает проверку наличия сертификатов НУЦ Минцифры
    verify_ssl_certs=False,
    streaming=False,
)

messages = [
    SystemMessage(
        content="Ты эмпатичный бот-психолог, который помогает пользователю решить его проблемы."
    )
]

while(True):
    user_input = input("Пользователь: ")
    messages.append(HumanMessage(content=user_input))
    res = llm.invoke(messages)
    messages.append(res)
    print("GigaChat: ", res.content)
```

Объект GigaChat принимает параметры:

* `credentials` — авторизационные данные для обмена сообщениями с GigaChat API. О том, как их получить — в разделе [Быстрый старт](https://developers.sber.ru/docs/ru/gigachat/individuals-quickstart).
* `scope` — необязательный параметр, в котором можно указать версию API. Возможные значения:
  
  * `GIGACHAT_API_PERS` — версия API для физических лиц;
  * `GIGACHAT_API_B2B` — доступ для ИП и юридических лиц по предоплате;
  * `GIGACHAT_API_CORP` — доступ для ИП и юридических лиц по постоплате.

  По умолчанию запросы передаются в версию для физических лиц.

* `model` — необязательный параметр, в котором можно явно задать [модель GigaChat](https://developers.sber.ru/docs/ru/gigachat/models). По умолчанию запросы передаются в модель `GigaChat`.
* `verify_ssl_certs` — необязательный параметр, с помощью которого можно отключить проверку [сертификатов НУЦ Минцифры](/https://developers.sber.ru/docs/ru/gigachat/certificates).
* `streaming` — необязательный параметр, который включает и отключает [потоковую генерацию токенов](https://developers.sber.ru/docs/ru/gigachat/api/response-token-streaming). Потоковая генерация позволяет повысить отзывчивость интерфейса программы при [работе с длинными текстами](#Работа-с-большими-текстами). По умолчанию `False`.

## Вспомогательные функции

### Показать список доступных моделей

Полный список доступных моделей можно получить с помощью метода `get_models()`.

```py
llm = GigaChat(
  credentials="авторизационные_данные",
  verify_ssl_certs=False,
)
llm.get_models() 
```

Метод выполняет запрос [`GET /models`](https://developers.sber.ru/docs/ru/gigachat/api/reference/rest/get-models) к GigaChat API и возвращает список с описанием доступных моделей.


> [!WARNING]
> Стоимость запросов к разным моделям отличается. Подробную информацию о тарификации запросов к той или иной модели вы ищите в [официальной документации](https://developers.sber.ru/docs/ru/gigachat/api/tariffs).

### Посчитать токены в запросе

Для подсчета количества токенов в запросе используйте метод `get_num_tokens(str)`:

```py
llm = GigaChat(
  credentials="авторизационные_данные",
  verify_ssl_certs=False,
)
llm.get_num_tokens("Сколько токенов в этой строке?")
```

Метод выполняет запрос [`POST /tokens/count`](https://developers.sber.ru/docs/ru/gigachat/api/reference/rest/post-tokens-count) к GigaChat API и возвращает информацию о количестве токенов в строке.

## Устранение проблем

Если у вас возникли проблемы при работе с GigaChain убедитесь, что:

- у вас установлена последняя версия библиотеки (v0.2.16+);
- вместо модулей GigaChain не установлены модули LangChain.

Одновременное использование библиотек LangChain и GigaChain вызывает конфликты, которые могут проявиться даже после полного удаления одной из библиотек.
Для предотвращения конфликтов рекомендуется создать чистое виртуальное окружение Python и установить только пакеты, которые входят в состав GigaChain.
Подробнее — в разделе [Миграция с LangChain](#Миграция-с-LangChain).

Для вывода полного списка установленных модулей используйте команду:

```shell
pip list
```

В выводе команды не должно быть модулей, которые содержат в названии слово `langchain`.

> [!NOTE]
> Исключение составляют модули `langchain_hub` и `langsmith`. Они не требуют удаления и переустановки.

### Миграция с LangChain

Самый надежный способ избежать проблем при миграции с LangChain — использовать новое виртуальное окружение Python (*Python virtual environment*), в котором никогда не устанавливались пакеты LangChain.

Чтобы создать новое виртуальное окружение [venv](https://docs.python.org/3/library/venv.html), используйте команды:

```sh
# Создает чистое виртуальное окружение Python
python -m venv .venv
# Активирует созданное окружение
source .venv/bin/activate
# Устанавливает gigachain
pip install gigachain-community
```

### Работа с большими текстами

Обработка больших текстов может занимать у модели продолжительное время — 10 минут и более.
Это может привести к возникновению проблем, связанных с превышением времени ожидания.

Чтобы избежать таких проблем, используйте [потоковую передачу токенов](https://developers.sber.ru/docs/ru/gigachat/api/response-token-streaming) (параметр `streaming=True`):

```py
llm = GigaChat(
  credentials="<авторизационные_данные>",
  verify_ssl_certs=False,
  streaming=True,
)
```