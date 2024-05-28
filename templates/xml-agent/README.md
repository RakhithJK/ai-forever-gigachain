
# xml-agent

This package creates an agent that uses XML syntax to communicate its decisions of what actions to take. It uses Anthropic's Claude models for writing XML syntax and can optionally look up things on the internet using DuckDuckGo.

## Environment Setup

Two environment variables need to be set:

- `ANTHROPIC_API_KEY`: Required for using Anthropic

## Usage

To use this package, you should first have the LangChain CLI installed:

```shell
<<<<<<< HEAD
pip install -U "gigachain-cli"
=======
pip install -U langchain-cli
>>>>>>> langchan/master
```

To create a new LangChain project and install this as the only package, you can do:

```shell
<<<<<<< HEAD
gigachain app new my-app --package xml-agent
=======
langchain app new my-app --package xml-agent
>>>>>>> langchan/master
```

If you want to add this to an existing project, you can just run:

```shell
<<<<<<< HEAD
gigachain app add xml-agent
=======
langchain app add xml-agent
>>>>>>> langchan/master
```

And add the following code to your `server.py` file:
```python
from xml_agent import agent_executor as xml_agent_chain

add_routes(app, xml_agent_chain, path="/xml-agent")
```

(Optional) Let's now configure LangSmith. 
LangSmith will help us trace, monitor and debug LangChain applications. 
You can sign up for LangSmith [here](https://smith.langchain.com/). 
If you don't have access, you can skip this section


```shell
export LANGCHAIN_TRACING_V2=true
export LANGCHAIN_API_KEY=<your-api-key>
export LANGCHAIN_PROJECT=<your-project>  # if not specified, defaults to "default"
```

If you are inside this directory, then you can spin up a LangServe instance directly by:

```shell
<<<<<<< HEAD
gigachain serve
=======
langchain serve
>>>>>>> langchan/master
```

This will start the FastAPI app with a server is running locally at 
[http://localhost:8000](http://localhost:8000)

We can see all templates at [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)
We can access the playground at [http://127.0.0.1:8000/xml-agent/playground](http://127.0.0.1:8000/xml-agent/playground)  

We can access the template from code with:

```python
from langserve.client import RemoteRunnable

runnable = RemoteRunnable("http://localhost:8000/xml-agent")
```
