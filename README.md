<<<<<<< HEAD
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

## 🤔 Что такое GigaChain?

**GigaChain** это фреймворк для разработки приложений с использованием больших языковых моделей (*LLM*), таких как `GigaChat` или `YandexGPT`. Он позволяет создавать приложения, которые:
- **Учитывают контекст**: подключите свою модель к источникам данных
- **Могут рассуждать**: Положитесь на модель в построении рассуждениях (о том, как ответить, опираясь на контекст, какие действия предпринять и т.д.)

> [!WARNING]
> Версия библиотеки [LangChain](https://github.com/langchain-ai/langchain) адаптированная для русского языка с поддержкой нейросетевой модели [GigaChat](https://developers.sber.ru/portal/products/gigachat).
> Библиотека GigaChain обратно совместима с LangChain, что позволяет использовать ее не только для работы с [GigaChat](#примеры-работы-с-gigachat), но и при работе с [другими LLM](#примеры-работы-с-другими-llm) в различных комбинациях.

Фреймворк включает:

- **Библиотеку GigaChain**. Библиотека на Python содержит интерфейсы и интеграции для множества компонентов, базовую среду выполнения для объединения этих компонентов в цепочки и агенты, а также готовые реализации цепочек и агентов.
- **[Хаб промптов](hub)**. Набор типовых отлаженных промптов для решения различных задач.
- **[GigaChain Templates](templates)**. Коллекция легко развертываемых шаблонных решений для широкого спектра задач.
- **[GigaServe](https://github.com/ai-forever/gigaserve)**. Библиотека, позволяющая публиковать цепочки GigaChain в форме REST API.
- **[GigaGraph](https://github.com/ai-forever/gigagraph)**. Библиотека, дающая возможность работать с LLM (большими языковыми моделями), для создания приложений, которые используют множество взаимодействующих цепочек (акторов) и сохраняют данные о состоянии. Так как в основе GigaGraph лежит GigaChain, предполагается совместное использование обоих библиотек.

Кроме этого, фреймворк совместим со сторонним сервисом [LangSmith](https://smith.langchain.com) — платформой для разработчиков, которая позволяет отлаживать, тестировать, оценивать и отслеживать цепочки, построенные на любой платформе LLM, и легко интегрируется с LangChain и GigaChain..

Репозиторий содержит следующие компоненты:

* [`gigachain`](libs/langchain);
* [`gigachain-core`](libs/core);
* [`gigachain-community`](libs/community);
* [`gigachain-experimental`](libs/experimental);
* [`gigachain-cli`](libs/cli);
* [`GigaChain Templates`](templates) и пакеты Python.

![Стэк технологий GigaChain](docs/static/img/gigachain-stack.png)

> [!WARNING]
> GigaChain находится в состоянии альфа-версии: мы заняты переводом библиотеки и ее адаптацией для работы с GigaChat. Будьте осторожны при использовании GigaChain в своих проектах, так как далеко не все компоненты оригинальной библиотеки проверены на совместимость с GigaChat.
> 
> Будем рады вашим PR и issues.

Библиотека упростит интеграцию вашего приложения с нейросетевой моделью GigaChat и поможет в следующих задачах:

- Работа с промптами и LLM.

  Включая управление промптами и их оптимизацию. GigaChain предоставляет универсальный интерфейс для всех LLM, а также стандартные инструменты для работы с ними.

  Пример - [Работа с хабом промптов на примере задачи суммаризации книг](hub/prompts/summarize/map_reduce/summarize_examples.ipynb)

- Создание цепочек (*Chains*).

  Цепочки представляют собой последовательность вызовов к LLM и/или другим инструментам. GigaChain предоставляет стандартный интерфейс для создания цепочек, различные интеграции с другими инструментами и готовые цепочки для популярных приложений.

- Дополнение данных (*Data Augmented Generation*).

  Генерация с дополнением данными включает в себя специфические типы цепочек, которые сначала получают данные от внешнего источника, а затем используют их в генерации. Примеры включают в себя суммирование больших текстов и ответы на вопросы по заданным источникам данных.

  Пример - [Ответы на вопросы по документу на примере "разговор с книгой" (RAG)](docs/docs/how_to/gigachat_qa.ipynb)
  
  Пример — [Ответы на вопросы по статьям из Wikipedia](docs/docs/integrations/retrievers/wikipedia.ipynb)

- Работа с агентами (*Agents*).

  Агент представляет собой LLM, которая принимает решение о дальнейшем действии, отслеживает его результат, и, с учетом результата, принимает следующее решение. Процесс повторяется до завершения. GigaChain предоставляет стандартный интерфейс для работы с агентами, выбор агентов и примеры готовых агентов.

  Пример — [CAMEL агент для разработки программ](cookbook/camel_role_playing.ipynb)

- Создание памяти.

  Память сохраняет состояние между вызовами цепочки или агента. GigaChain предоставляет стандартный интерфейс для создания памяти, коллекцию реализаций памяти и примеры цепочек и агентов, которые используют память.

- Самооценка (*Evaluation*).

  **BETA** Генеративные модели традиционно сложно оценивать с помощью стандартных метрик. Один из новых способов оценки — использование самих языковых моделей. GigaChain предоставляет некоторые запросы и цепочки для решения таких задач


## Установка

Библиотеку можно установить с помощью pip:

```sh
pip install gigachain
```

### Миграция с LangChain

Для миграции с LangChain и начала использования GigaChain нужно удалить все компоненты библиотеки `langchain`:

```sh
pip uninstall langchain langchain_experimental langchain_core langchain_community
```

После чего установить библиотеку `gigachain`:

```sh
pip install gigachain
```

## Работа с GigaChain

Основной особенностью библиотеки является наличие модуля [`gigachat`](#описание-объекта-gigachain), который позволяет отправлять запросы к нейросетевой модели GigaChat.

### Авторизация запросов к GigaChat

Для авторизации запросов к GigaChat вам понадобится получить авторизационные данные для работы с GigaChat API.

> [!NOTE]
> О том как получить авторизационные данные для доступа к GigaChat читайте в [официальной документации](https://developers.sber.ru/docs/ru/gigachat/api/integration).

Для работы с сервисом GigaChat передайте полученные авторизационные данные в параметре `credentials` объекта `GigaChat`.

```py
chat = GigaChat(credentials=<авторизационные_данные>)
```

Для обращения к GigaChat в вашем приложении или в вашей ОС должны быть установлены сертификаты НУЦ Минцифры. О том как настроить сертификаты НУЦ Минцифры для обращения к GigaChat читайте в [официальной документации](https://developers.sber.ru/docs/ru/gigachat/certificates).

Вы можете установить сертификаты с помощью утилиты [`gigachain-cli`](libs/cli).
Для этого:

1. Установите утилиту с помощью менеджера пакетов pip:

```sh
pip install gigachain-cli
```

2. Установите сертификаты с помощью команды:

```sh
gigachain install-rus-certs
```

Если вы не используете сертификат НУЦ Минцифры, то при создании объекта `GigaChat` вам нужно передать параметр `verify_ssl_certs=False` .

```py
chat = GigaChat(credentials=<авторизационные_данные>, verify_ssl_certs=False)
```

> [!NOTE]
> Для передачи аторизационных данных и других параметров GigaChat вы также можете настроить переменные окружения, например, `GIGACHAT_CREDENTIALS`, `GIGACHAT_GIGACHAT_` и другие.

### Использование модуля gigachat

Вот простой пример работы с чатом с помощью модуля:

```py
"""Пример работы с чатом через gigachain"""
from langchain.schema import HumanMessage, SystemMessage
from langchain.chat_models.gigachat import GigaChat

# Авторизация в сервисе GigaChat
chat = GigaChat(credentials=<авторизационные_данные>, verify_ssl_certs=False)

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

Развернутую версию примера смотрите в notebook [Работа с GigaChat](docs/extras/integrations/chat/gigachat.ipynb). Здесь же показан пример работы со стримингом.

Больше примеров в [коллекции](#коллекция-примеров).

### Выбор модели

С помощью GigaChain вы можете обращаться к различным моделям, которые предоставляет GigaChat

Для этого передайте название модели в параметре `model`:

```py
chat = GigaChat(model="GigaChat-Pro", credentials=<авторизационные_данные>, verify_ssl_certs=False)
```

Полный список доступных моделей можно получить с помощью метода `get_models()`.

```py
chat = GigaChat(credentials=<авторизационные_данные>, verify_ssl_certs=False)
chat.get_models() 
```

Метод выполняет запрос [`GET /models`](https://developers.sber.ru/docs/ru/gigachat/api/reference#get-models) к GigaChat API и возвращает список с описанием доступных моделей.


> [!WARNING]
> Стоимость запросов к разным моделям отличается. Подробную информацию о тарификации запросов к той или иной модели вы ищите в [официальной документации](https://developers.sber.ru/docs/ru/gigachat/api/tariffs).

### Подсчет количества токенов

Для подсчета количества токенов в запросе используйте метод `get_num_tokens(str)`:

```py
chat = GigaChat(credentials=<авторизационные_данные>, verify_ssl_certs=False)
chat.get_num_tokens("Сколько токенов в этой строке")
```

Метод выполняет запрос [`POST /tokens/count`](https://developers.sber.ru/docs/ru/gigachat/api/reference#post-tokens-count) к GigaChat API и возвращает информацию о количестве токенов в строке.

## Описание модуля gigachat

Модуль [`gigachat`](libs/langchain/langchain/chat_models/gigachat.py) позволяет авторизовать запросы от вашего приложения в GigaChat с помощью GigaChat API. Модуль поддерживает работу как в синхронном, так и в асинхронном режиме. Кроме этого модуль поддерживает обработку [потоковой передачи токенов](https://developers.sber.ru/docs/ru/gigachat/api/response-token-streaming)[^1].

> [!NOTE]
> Как подключить GigaChat API читайте в [официальной документации](https://developers.sber.ru/docs/ru/gigachat/api/integration).

Модуль поддерживает не только GigaChat. Поэтому, если ваше приложение уже использует другие нейросетевые модели, интеграция с GigaChat не составит труда.

## Работа с эмбеддингами

Эмбеддинг — это векторное представление слова, которое можно использовать для определения смысловой близости разных текстов. 
Векторное представление создается с помощью модели [Embeddings](https://developers.sber.ru/docs/ru/gigachat/models#model-dlya-vektornogo-predstavleniya-teksta).

> [!NOTE]
> Работа с моделью Embeddings оплачивается отдельно. Подробнее — в разделе [Тарифы и оплата](https://developers.sber.ru/docs/ru/gigachat/api/tariffs).

Для создания эмбеддингов с помощью GigaChain используйте модуль `GigaChatEmbeddings`:

```python
from langchain_community.embeddings.gigachat import GigaChatEmbeddings

embeddings = GigaChatEmbeddings(
    credentials="<авторизационные_данные>", verify_ssl_certs=False
)
```

Для работы с `GigaChatEmbeddings` используются те же авторизационные данные, что и при [работе с модулем GigaChat](#авторизация-запросов-к-gigachat).

Подробнее о работе с эмбеддингами и использовании их при реализации RAG-методики — в разделе [Ответы на вопросы с помощью RAG](/docs/docs/use_cases/question_answering/index.ipynb).

## Устранение проблем

Если у вас возникли проблемы при работе с GigaChain убедитесь, что:

- у вас установлена последняя версия библиотеки;
- вместо модулей GigaChain не установлены модули LangChain.

В любом случае для решения проблемы нужно удалить модули LangChain и повторно установить последние версии модулей GigaChain.

Для вывода полного списка установленных модулей используйте команду:

```shell
pip list
```

> [!NOTE]
> Модули `langchain_hub` и `langsmith` не требуют удаления и переустановки.

Для удаления модулей LangChain используйте команды менеджера пакетов:

```shell
pip uninstall langchain_core
pip uninstall langchain_community
pip uninstall langchain_experimental
#Модуль langchain_openai содержит зависимости от langchain_core
pip uninstall langchain_openai
pip uninstall langchain
```

> [!WARNING]
> Если кроме представленных в примере модулей вы используете модули `langgraph` и `langserve` их также потребуется заменить на `gigagraph` и `gigaserve`, соответственно.

Для установки последних версий модулей GigaChain используйте команды менеджера пакетов:

```shell
pip install -U gigachain_core
pip install -U gigachain_community
pip install -U gigachain_experimental
pip install -U gigachain_openai
pip install -U gigachain
```

### Работа с большими текстами

Обработка больших текстов может занимать у модели продолжительное время — 10 минут и более.
Это может привести к возникновению проблем, связанных с превышением времени ожидания.

Чтобы избежать таких проблем, используйте [потоковую передачу токенов](/ru/gigachat/api/response-token-streaming) (параметр `streaming=True`):

```py
chat = GigaChat(credentials='<авторизационные_данные>', verify_ssl_certs=False, streaming=True)
```

## Коллекция примеров

Ниже представлен список примеров использования GigaChain.

### Базовые примеры работы с GigaChat

- [Ответы на вопросы по документу на примере "разговор с книгой" (RAG)](docs/docs/how_to/gigachat_qa.ipynb)
- [Суммаризация по алгоритму MapReduce](docs/extras/use_cases/summarization.ipynb) (см. раздел map/reduce)
- [Работа с хабом промптов, цепочками и парсером JSON](docs/docs/modules/model_io/output_parsers/json.ipynb)
- [Работа с хабом промптов на примере задачи суммаризации книг](hub/prompts/summarize/map_reduce/summarize_examples.ipynb)
- [Парсинг списков, содержащихся в ответе](docs/docs/modules/model_io/output_parsers/list.ipynb)
- [Асинхронная работа с LLM](docs/docs/modules/model_io/llms/async_llm.ipynb)
- [Использование Elastic для поиска ответов по документам](docs/docs/integrations/retrievers/elastic_qna.ipynb)
- [Использование разных эмбеддингов для Retrieval механизма](docs/docs/modules/chains/how_to/retrieve.ipynb)
- [Генерация и выполнение кода с помощью PythonREPL](docs/docs/expression_language/cookbook/code_writing.ipynb)
- [Работа с кэшем в GigaChain](docs/docs/integrations/llms/gigachain_caching.ipynb)
- [CAMEL агент для разработки программ](cookbook/camel_role_playing.ipynb)
- [Автономный агент AutoGPT с использованием GigaChat](cookbook/autogpt/autogpt.ipynb)
- [Генерация плейлистов с помощью GigaChain и Spotify](docs/docs/modules/agents/how_to/playlists.ipynb)
- Работа с LlamaIndex: [с помощью ретривера и QA цепочки](docs/docs/integrations/retrievers/llama_index_retriever.ipynb) / [с помощью тула и Conversational агента](docs/docs/modules/agents/tools/llama_index_tool.ipynb)
- [Агент-риелтор на GigaChat functions](cookbook/realestate/realestate.ipynb)

### Развлекательные примеры
- [Площадка для споров между GigaChat и YandexGPT с судьей GPT-4](docs/docs/use_cases/fun/debates.ipynb)
- [Игра Blade Runner: GPT-4 и GigaChat выясняют, кто из них бот](docs/docs/use_cases/fun/blade_runner.ipynb)
- [Игра в стиле DnD с GPT-3.5 и GigaChat](docs/docs/use_cases/question_answering/agent_simulations/multi_llm_thre_player_dnd.ipynb)

### Примеры работы с другими LLM

- [Агент-менеджер по продажам с автоматическим поиском по каталогу и формированием заказа](docs/docs/modules/agents/how_to/add_memory_openai_functions.ipynb)
- [Поиск ответов в интернете с автоматическими промежуточными вопросами (self-ask)](docs/docs/modules/agents/agent_types/self_ask_with_search.ipynb)
- [Пример использования YandexGPT](docs/docs/integrations/chat/yandex.ipynb)

### Примеры приложений для Streamlit

- [Чат-бот на базе GigaChat с потоковой генерацией и разными видами авторизации](libs/streamlit_agent/gigachat_streaming.py) [Try demo](https://gigachat-streaming.streamlit.app/)

### Примеры сторонних приложений, использующих GigaChain

- [GigaShell - copilot для командной строки](https://github.com/Rai220/GigaShell)

## Участие в проекте

GigaChain — это проект с открытым исходным кодом в быстроразвивающейся области. Мы приветствуем любое участие в разработке, развитии инфраструктуры или улучшении документации.
[BETA] Генеративные модели, как известно, трудно оценить с помощью традиционных показателей. Одним из новых способов их оценки является использование для оценки самих языковых моделей. LangChain предоставляет несколько подсказок/цепочек для помощи в этом.

[Подробнее о том, как внести свой вклад](.github/CONTRIBUTING.md).

## 📖 Дополнительная документация

> [!NOTE]
> Полная документация GigaChain находится в процессе перевода.
> Вы можете также пользоваться [документацией LangChain](https://python.langchain.com), поскольку GigaChain совместим с LangChain:
=======
# 🦜️🔗 LangChain

⚡ Build context-aware reasoning applications ⚡

[![Release Notes](https://img.shields.io/github/release/langchain-ai/langchain)](https://github.com/langchain-ai/langchain/releases)
[![CI](https://github.com/langchain-ai/langchain/actions/workflows/check_diffs.yml/badge.svg)](https://github.com/langchain-ai/langchain/actions/workflows/check_diffs.yml)
[![Downloads](https://static.pepy.tech/badge/langchain-core/month)](https://pepy.tech/project/langchain-core)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Twitter](https://img.shields.io/twitter/url/https/twitter.com/langchainai.svg?style=social&label=Follow%20%40LangChainAI)](https://twitter.com/langchainai)
[![](https://dcbadge.vercel.app/api/server/6adMQxSpJS?compact=true&style=flat)](https://discord.gg/6adMQxSpJS)
[![Open in Dev Containers](https://img.shields.io/static/v1?label=Dev%20Containers&message=Open&color=blue&logo=visualstudiocode)](https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/langchain-ai/langchain)
[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/langchain-ai/langchain)
[![GitHub star chart](https://img.shields.io/github/stars/langchain-ai/langchain?style=social)](https://star-history.com/#langchain-ai/langchain)
[![Dependency Status](https://img.shields.io/librariesio/github/langchain-ai/langchain)](https://libraries.io/github/langchain-ai/langchain)
[![Open Issues](https://img.shields.io/github/issues-raw/langchain-ai/langchain)](https://github.com/langchain-ai/langchain/issues)

Looking for the JS/TS library? Check out [LangChain.js](https://github.com/langchain-ai/langchainjs).

To help you ship LangChain apps to production faster, check out [LangSmith](https://smith.langchain.com). 
[LangSmith](https://smith.langchain.com) is a unified developer platform for building, testing, and monitoring LLM applications. 
Fill out [this form](https://www.langchain.com/contact-sales) to speak with our sales team.

## Quick Install

With pip:
```bash
pip install langchain
```

With conda:
```bash
conda install langchain -c conda-forge
```

## 🤔 What is LangChain?

**LangChain** is a framework for developing applications powered by large language models (LLMs).

For these applications, LangChain simplifies the entire application lifecycle:

- **Open-source libraries**: Build your applications using LangChain's [modular building blocks](https://python.langchain.com/docs/expression_language/) and [components](https://python.langchain.com/docs/modules/). Integrate with hundreds of [third-party providers](https://python.langchain.com/docs/integrations/platforms/).
- **Productionization**: Inspect, monitor, and evaluate your apps with [LangSmith](https://python.langchain.com/docs/langsmith/) so that you can constantly optimize and deploy with confidence.
- **Deployment**: Turn any chain into a REST API with [LangServe](https://python.langchain.com/docs/langserve).

### Open-source libraries
- **`langchain-core`**: Base abstractions and LangChain Expression Language.
- **`langchain-community`**: Third party integrations.
  - Some integrations have been further split into **partner packages** that only rely on **`langchain-core`**. Examples include **`langchain_openai`** and **`langchain_anthropic`**.
- **`langchain`**: Chains, agents, and retrieval strategies that make up an application's cognitive architecture.
- **[`LangGraph`](https://python.langchain.com/docs/langgraph)**: A library for building robust and stateful multi-actor applications with LLMs by modeling steps as edges and nodes in a graph.

### Productionization:
- **[LangSmith](https://python.langchain.com/docs/langsmith)**: A developer platform that lets you debug, test, evaluate, and monitor chains built on any LLM framework and seamlessly integrates with LangChain.

### Deployment:
- **[LangServe](https://python.langchain.com/docs/langserve)**: A library for deploying LangChain chains as REST APIs.

![Diagram outlining the hierarchical organization of the LangChain framework, displaying the interconnected parts across multiple layers.](docs/static/svg/langchain_stack.svg "LangChain Architecture Overview")

## 🧱 What can you build with LangChain?

**❓ Question answering with RAG**

- [Documentation](https://python.langchain.com/docs/use_cases/question_answering/)
- End-to-end Example: [Chat LangChain](https://chat.langchain.com) and [repo](https://github.com/langchain-ai/chat-langchain)

**🧱 Extracting structured output**

- [Documentation](https://python.langchain.com/docs/use_cases/extraction/)
- End-to-end Example: [SQL Llama2 Template](https://github.com/langchain-ai/langchain-extract/)

**🤖 Chatbots**

- [Documentation](https://python.langchain.com/docs/use_cases/chatbots)
- End-to-end Example: [Web LangChain (web researcher chatbot)](https://weblangchain.vercel.app) and [repo](https://github.com/langchain-ai/weblangchain)

And much more! Head to the [Use cases](https://python.langchain.com/docs/use_cases/) section of the docs for more.

## 🚀 How does LangChain help?
The main value props of the LangChain libraries are:
1. **Components**: composable building blocks, tools and integrations for working with language models. Components are modular and easy-to-use, whether you are using the rest of the LangChain framework or not
2. **Off-the-shelf chains**: built-in assemblages of components for accomplishing higher-level tasks

Off-the-shelf chains make it easy to get started. Components make it easy to customize existing chains and build new ones. 

## LangChain Expression Language (LCEL)

LCEL is the foundation of many of LangChain's components, and is a declarative way to compose chains. LCEL was designed from day 1 to support putting prototypes in production, with no code changes, from the simplest “prompt + LLM” chain to the most complex chains.

- **[Overview](https://python.langchain.com/docs/expression_language/)**: LCEL and its benefits
- **[Interface](https://python.langchain.com/docs/expression_language/interface)**: The standard interface for LCEL objects
- **[Primitives](https://python.langchain.com/docs/expression_language/primitives)**: More on the primitives LCEL includes

## Components

Components fall into the following **modules**:

**📃 Model I/O:**

This includes [prompt management](https://python.langchain.com/docs/modules/model_io/prompts/), [prompt optimization](https://python.langchain.com/docs/modules/model_io/prompts/example_selectors/), a generic interface for [chat models](https://python.langchain.com/docs/modules/model_io/chat/) and [LLMs](https://python.langchain.com/docs/modules/model_io/llms/), and common utilities for working with [model outputs](https://python.langchain.com/docs/modules/model_io/output_parsers/).

**📚 Retrieval:**

Retrieval Augmented Generation involves [loading data](https://python.langchain.com/docs/modules/data_connection/document_loaders/) from a variety of sources, [preparing it](https://python.langchain.com/docs/modules/data_connection/document_loaders/), [then retrieving it](https://python.langchain.com/docs/modules/data_connection/retrievers/) for use in the generation step.

**🤖 Agents:**

Agents allow an LLM autonomy over how a task is accomplished. Agents make decisions about which Actions to take, then take that Action, observe the result, and repeat until the task is complete done. LangChain provides a [standard interface for agents](https://python.langchain.com/docs/modules/agents/), a [selection of agents](https://python.langchain.com/docs/modules/agents/agent_types/) to choose from, and examples of end-to-end agents.

## 📖 Documentation

Please see [here](https://python.langchain.com) for full documentation, which includes:
>>>>>>> langchan/master

- [Getting started](https://python.langchain.com/docs/get_started/introduction): installation, setting up the environment, simple examples
- [Use case](https://python.langchain.com/docs/use_cases/) walkthroughs and best practice [guides](https://python.langchain.com/docs/guides/)
- Overviews of the [interfaces](https://python.langchain.com/docs/expression_language/), [components](https://python.langchain.com/docs/modules/), and [integrations](https://python.langchain.com/docs/integrations/providers)

You can also check out the full [API Reference docs](https://api.python.langchain.com).

## 🌐 Ecosystem

- [🦜🛠️ LangSmith](https://python.langchain.com/docs/langsmith/): Tracing and evaluating your language model applications and intelligent agents to help you move from prototype to production.
- [🦜🕸️ LangGraph](https://python.langchain.com/docs/langgraph): Creating stateful, multi-actor applications with LLMs, built on top of (and intended to be used with) LangChain primitives.
- [🦜🏓 LangServe](https://python.langchain.com/docs/langserve): Deploying LangChain runnables and chains as REST APIs.
  - [LangChain Templates](https://python.langchain.com/docs/templates/): Example applications hosted with LangServe.

<<<<<<< HEAD
## Лицензия

Проект распространяется по лицензии MIT, доступной в файле `LICENSE`.

[^1]: В настоящий момент эта функциональность доступна в бета-режиме.
=======

## 💁 Contributing

As an open-source project in a rapidly developing field, we are extremely open to contributions, whether it be in the form of a new feature, improved infrastructure, or better documentation.

For detailed information on how to contribute, see [here](https://python.langchain.com/docs/contributing/).

## 🌟 Contributors

[![langchain contributors](https://contrib.rocks/image?repo=langchain-ai/langchain&max=2000)](https://github.com/langchain-ai/langchain/graphs/contributors)
>>>>>>> langchan/master
