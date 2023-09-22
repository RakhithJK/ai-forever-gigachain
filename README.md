[![CI](https://github.com/ai-forever/gigachain/actions/workflows/langchain_ci.yml/badge.svg)](https://github.com/ai-forever/gigachain/actions/workflows/langchain_ci.yml)
[![Downloads](https://static.pepy.tech/badge/gigachain/month)](https://pepy.tech/project/gigachain)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

<br />
<div align="center">

  <h1 align="center">🦜️🔗 GigaChain (GigaChat + LangChain)</h1>

  <p align="center">
    Библиотека для разработки LangChain-style приложений на русском языке с поддержкой GigaChat
    <br />
    <a href="https://github.com/ai-forever/gigachain/issues">Создать issue</a>
    ·
    <a href="https://developers.sber.ru/docs/ru/gigachat/overview">Документация GigaChat</a>
  </p>
</div>


## О проекте

Версия библиотеки [LangChain](https://github.com/langchain-ai/langchain) адаптированная для русского языка с поддержкой нейросетевой модели [GigaChat](https://developers.sber.ru/portal/products/gigachat).

Библиотека GigaChain обратно совместима с LangChain, что позволяет использовать ее не только для работы с [GigaChat](#примеры-работы-с-gigachat), но и при работе с [другими LLM](#примеры-работы-с-другими-llm) в различных комбинациях.

> [!WARNING]
> GigaChain находится в состоянии альфа-версии: мы заняты переводом библиотеки и ее адаптацией для работы с GigaChat. Будьте осторожны при использовании GigaChain в своих проектах, так как далеко не все компоненты оригинальной библиотеки проверены на совместимость с GigaChat.
> 
> Будем рады вашим PR и issues.

Библиотека упростит интеграцию вашего приложения с нейросетевой моделью GigaChat и поможет в следующих задачах:

- Работа с промптами и LLM.

  Включая управление промптами и их оптимизацию. GigaChain предоставляет универсальный интерфейс для всех LLM, а также стандартные инструменты для работы с ними.

- Создание цепочек (*Chains*).

  Цепочки представляют собой последовательность вызовов к LLM и/или другим инструментам. GigaChain предоставляет стандартный интерфейс для создания цепочек, различные интеграции с другими инструментами и готовые цепочки для популярных приложений.

- Дополнение данных (*Data Augmented Generation*).

  Генерация с дополнением данными включает в себя специфические типы цепочек, которые сначала получают данные от внешнего источника, а затем используют их в генерации. Примеры включают в себя суммирование больших текстов и ответы на вопросы по заданным источникам данных.

  Пример — [Ответы на вопросы по статьям из wikipedia](https://github.com/ai-forever/gigachain/blob/master/docs/extras/integrations/retrievers/wikipedia.ipynb)

- Работа с агентами (*Agents*).

  Агент представляет собой LLM, которая принимает решение о дальнейшем действии, отслеживает его результат, и, с учетом результата, принимает следующее решение. Процесс повторяется до завершения. GigaChain предоставляет стандартный интерфейс для работы с агентами, выбор агентов и примеры готовых агентов.

  Пример — [Игра в стиле DnD с GPT-3.5 и GigaChat](docs/extras/use_cases/agent_simulations/multi_llm_thre_player_dnd.ipynb).

- Создание памяти.

  Память сохраняет состояние между вызовами цепочки или агента. GigaChain предоставляет стандартный интерфейс для создания памяти, коллекцию реализаций памяти и примеры цепочек и агентов, которые используют память.

- Самооценка (*Evaluation*).

  **BETA** Генеративные модели традиционно сложно оценивать с помощью стандартных метрик. Один из новых способов оценки — использование самих языковых моделей. GigaChain предоставляет некоторые запросы и цепочки для решения таких задач.

> [!WARNING]
> GigaChain наследует [несовместимые изменения](https://github.com/langchain-ai/langchain#breaking-changes-for-select-chains-sqldatabase-on-72823), которые были сделаны в оригинальной библиотеке 28.07.2023. Подробнее о том, как мигрировать свой проект читайте в [документации Langchain](https://github.com/langchain-ai/langchain/blob/master/MIGRATE.md).


## Установка

Библиотеку можно установить с помощью pip:

```sh
pip install gigachain
```

## Работа с GigaChain

Основной особенностью библиотеки является наличие модуля [`gigachat`](#описание-объекта-gigachain), который позволяет обращаться к нейросетевой модели GigaChat.

> [!NOTE]
> О том как подключить GigaChat читайте в [официальной документации](https://developers.sber.ru/docs/ru/gigachat/api/integration).

Вот простой пример работы с чатом с помощью модуля:

```py
"""Пример работы с чатом через gigachain"""
from langchain.schema import HumanMessage, SystemMessage
from langchain.chat_models.gigachat import GigaChat

# Авторизация в сервисе GigaChat
chat = GigaChat(user=<user_name>, password=<password>)

messages = [
    SystemMessage(
        content="Ты эмпатичный бот-психолог, который помогает пользователю решить его проблемы."
    )
]

while(True):
    user_input = input("User: ")
    messages.append(HumanMessage(content=user_input))
    res = chat(messages)
    messages.append(res)
    print("Bot: ", res.content)
```

Развернутую версию примера смотрите в notebook [Работа с GigaChat](docs/extras/integrations/chat/gigachat.ipynb).

Больше примеров в [коллекции](#коллекция-примеров). 

## Описание модуля gigachat

Модуль [`gigachat`](libs/langchain/langchain/chat_models/gigachat.py) позволяет авторизовать запросы от вашего приложения в GigaChat с помощью GigaChat API. Модуль поддерживает работу как в синхронном, так и в асинхронном режиме. Кроме этого модуль поддерживает обработку [потоковой передачи токенов](https://developers.sber.ru/docs/ru/gigachat/api/response-token-streaming)[^1].

> [!NOTE]
> Сейчас GigaChat API доступно только юридическим лицам и индивидуальным предпринимателям после подписания договора.
>
> Как подключить GigaChat API читайте в [официальной документации](https://developers.sber.ru/docs/ru/gigachat/api/integration).

Модуль поддерживает не только GigaChat. Поэтому, если ваше приложение уже использует другие нейросетевые модели, интеграция с GigaChat не составит труда.

> [!NOTE]
> Модуль не поддерживает работу с функциями, так как в настоящий момент они отсутствуют в GigaChat.

## Коллекция примеров

Ниже представлен список примеров использования GigaChain.

### Примеры работы с GigaChat

- [Ответы на вопросы по статьям из wikipedia](docs/extras/integrations/retrievers/wikipedia.ipynb)
- [Суммаризация map-reduce](docs/extras/use_cases/summarization.ipynb) (см. раздел map/reduce)
- [Игра Blade Runner: GPT-4 и GigaChat выясняют, кто из них бот](docs/extras/use_cases/more/fun/blade_runner.ipynb)
- [Работа с хабом промптов, цепочками и парсером JSON](docs/extras/modules/model_io/output_parsers/json.ipynb)
- [Игра в стиле DnD с GPT-3.5 и GigaChat](docs/extras/use_cases/agent_simulations/multi_llm_thre_player_dnd.ipynb)
- [Парсинг списков, содержащихся в ответе](docs/extras/modules/model_io/output_parsers/list.ipynb)
- [Асинхронная работа с LLM](docs/extras/modules/model_io/models/llms/async_llm.ipynb)
- [Использование Elastic для поиска ответов по документам](docs/extras/integrations/retrievers/elastic_qna.ipynb)

### Примеры работы с другими LLM

- [Агент-менеджер по продажам с автоматическим поиском по каталогу и формированием заказа](docs/extras/modules/agents/how_to/add_memory_openai_functions.ipynb)
- [Поиск ответов в интернете с автоматическими промежуточными вопросами (self-ask)](docs/extras/modules/agents/agent_types/self_ask_with_search.ipynb)

## Участие в проекте

GigaChain — это проект с открытым исходным кодом в быстроразвивающейся области. Мы приветствуем любое участие в разработке, развитии инфраструктуры или улучшении документации.

[Подробнее о том, как внести свой вклад](.github/CONTRIBUTING.md).

## Лицензия

Проект распространяется по лицензии MIT, доступной в файле `LICENSE`.

[^1]: В настоящий момент эта функциональность доступна в бета-режиме.
