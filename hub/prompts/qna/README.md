# Поиск по документам (вопрос-ответ)

Шаблоны промптов для генерации ответов на вопросы по переданным документам.

Здесь вы также найдёте шаблон промпта для ответов на экзаменационное тестирование.
Пример работы промпта — в блокноте, который демонстрирует [экзамен по правилам дорожного движения](/docs/extras/integrations/chat/examination.ipynb).

## Ответы на вопросы по документам
- `qna_basic_system.yaml` - простейший вариант вопрос-ответов по документам. (system-часть). В качестве user-части просто задайте свой вопрос.

- `qna_system.yaml` — поиск ответа на вопрос по документам (system-часть).
- `qna_user.yaml` — поиск ответа на вопрос по документам (user-часть).
- `qna_user_additional.yaml` - дополнительный вопрос по документам в рамках диалога.

## Ответы на вопросы по документам со ссылками на источники
- `qna_with_refs_system.yaml` — поиск ответа на вопрос по документам со сслыками на источники (system-часть).
- `qna_with_refs_user.yaml` — поиск ответа на вопрос по документам со сслыками на источники (user-часть).

## Дополнительные промпты
- `generate_question_prompt.yaml` — генерация вопросов к документу. Используется для улучшения качества индексации.

## Входные переменные

В зависимости от шаблона на вход промптам можно передавать следующие переменные:

- `question` — вопрос;
- `summaries` — данные, которые должны быть использованы в ответе.

## Пример использования

```python
from langchain.prompts import load_prompt
from langchain.chains import LLMChain

llm = ...hub/
qna_system_prompt = load_prompt('lc://prompts/qna/qna_system.yaml')
text = qna_system_prompt.format(text="... text of your documents ...")
```