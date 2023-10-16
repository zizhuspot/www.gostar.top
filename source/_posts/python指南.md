---
title:  LangChain完整指南 Python中的AI驱动语言建模
date: 2023-10-16 08:28:00
categories:
  - 语言驿站
tags:
  - LangChain
  - NLP
  - OpenAI
  - 模型集成
  - 文本分割
  - 语言模型
description: 本文介绍了LangChain这个强大的NLP Python库,它可以让我们创建和分析语言模型和智能代理。
cover: https://assets.zilliz.com/Conversational_Memory_in_Lang_Chain_7c1b4b7ba9.png
---

## 引言

在自然语言处理(NLP)领域,LangChain是一个功能强大的Python库,它赋予开发人员和研究人员创建、实验和分析语言模型和智能代理的能力。它提供了丰富的功能,可以从构建自定义模型到高效处理文本数据。本篇综合指南将深入介绍LangChain的重要组件,并演示如何在Python中发挥其强大的功能。


## 安装设置

在开始本指南之前,您需要创建一个新的文件夹,并使用pip安装LangChain和OpenAI库:

```
pip3 install langchain openai
```

## 代理

在LangChain中,**代理(Agent)**是一种可以理解和生成文本的实体。这些代理可以配置特定的行为和数据源,并经过训练以执行各种与语言相关的任务,使其成为广泛应用于各种应用的多功能工具。

### 创建LangChain代理

代理可以配置使用“工具”来收集所需的数据并生成良好的响应。以下是一个示例,它使用Serp API(互联网搜索API)来搜索与问题或输入相关的信息,并使用llm-math工具执行数学运算,例如单位转换或查找两个值之间的百分比变化:

```python
from langchain.agents import load_tools
from langchain.agents import initialize_agent
from langchain.agents import AgentType
from langchain.llms import OpenAI
import os

os.environ["OPENAI_API_KEY"] = "YOUR_OPENAI_API_KEY"
os.environ["SERPAPI_API_KEY"] = "YOUR_SERP_API_KEY"  # 在这里获取您的Serp API密钥:https://serpapi.com/

OpenAI.api_key = "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"
llm = OpenAI(model="gpt-3.5-turbo", temperature=0)
tools = load_tools(["serpapi", "llm-math"], llm=llm)
agent = initialize_agent(tools, llm, agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION, verbose=True)
agent.run("风力涡轮机在2022年全球产生了多少能量?")
```

在上面的代码中,我们首先进行了基本的导入和初始化LLM(llm = OpenAI(model="gpt-3.5-turbo", temperature=0)),然后使用tools = load_tools(["serpapi", "llm-math"], llm=llm)加载代理工作所需的工具。接下来,我们使用initialize_agent函数创建代理,给定指定的工具,并分配ZERO_SHOT_REACT_DESCRIPTION描述,这意味着它不会记得先前的问题。

#### 代理测试示例1

让我们使用以下输入对该代理进行测试:

```
"风力涡轮机在2022年全球产生了多少能量?"
```

如下图所示:

![](https://cdn.jsdelivr.net/gh/PirlosM/image@main/%E5%9B%BE%E7%89%871.png)

测试代理

如上所示,它使用以下逻辑:


- 使用Serp互联网搜索API搜索“2022年全球风力涡轮机能源产量”
- 分析最佳结果
- 获取任何相关的数字
- 使用 `llm-math` 工具将906吉瓦转换为焦耳,因为我们询问的是能量,而不是功率

#### 代理测试示例2

LangChain代理不限于搜索互联网。我们可以将几乎任何数据源(包括我们自己的数据源)连接到LangChain代理,并向其提问有关数据的问题。让我们尝试使用训练过的基于CSV数据集的代理。


从Kaggle上下载Netflix电影和电视节目数据集(由SHIVAM BANSAL提供),将其移动到您的目录中。现在将以下代码添加到一个新的Python文件中:

```python
from langchain.llms import OpenAI
from langchain.chat_models import ChatOpenAI
from langchain.agents.agent_types import AgentType
from langchain.agents import create_csv_agent
import os

os.environ["OPENAI_API_KEY"] = "YOUR_OPENAI_API_KEY"

agent = create_csv_agent(
    OpenAI(temperature=0), 
    "netflix_titles.csv",
    verbose=True,
    agent_type=AgentType.ZERO_SHOT_REACT_DESCRIPTION,
)

agent.run("Christian Bale出演了多少部电影?")
```

这段代码调用create_csv_agent函数,并使用netflix_titles.csv数据集。下图展示了我们的测试结果。

![](https://cdn.jsdelivr.net/gh/PirlosM/image@main/20231015184927.png)

正如上面所示,它的逻辑是在“cast”列中查找所有出现的“Christian Bale”。


我们还可以使用Pandas的Dataframe代理,代码如下:

```python
from langchain.agents import create_pandas_dataframe_agent
from langchain.chat_models import ChatOpenAI
from langchain.agents.agent_types import AgentType
from langchain.llms import OpenAI
import pandas as pd
import os

os.environ["OPENAI_API_KEY"] = "YOUR_OPENAI_KEY"
df = pd.read_csv("netflix_titles.csv")

agent = create_pandas_dataframe_agent(OpenAI(temperature=0), df, verbose=True)

agent.run("什么年份发布了最多的喜剧电影?")
```

如果运行此代码,将会得到类似下面的结果。

![](https://cdn.jsdelivr.net/gh/PirlosM/image@main/20231015184927.png)

![](https://cdn.jsdelivr.net/gh/PirlosM/image@main/20231015185147.png)

这只是一些示例。我们可以使用LangChain与几乎任何API或数据集进行集成。


## 模型

LangChain中有三种类型的模型:LLM、聊天模型和文本嵌入模型。让我们通过一些示例来探索每种模型的功能。

### 语言模型

LangChain提供了一种使用语言模型在Python中根据文本输入生成文本输出的方法。它没有聊天模型那么复杂,最适合用于简单的输入-输出语言任务。以下是使用OpenAI的示例:

```python
from langchain.llms import OpenAI
import os
os.environ["OPENAI_API_KEY"] = "YOUR_OPENAI_API_KEY"

llm = OpenAI(model="gpt-3.5-turbo", temperature=0.9)
print(llm("为Matt Nikonorov想一个说唱艺名"))
```

如上所示,它使用gpt-3.5-turbo模型根据提供的输入("为Matt Nikonorov想一个说唱艺名")生成输出。在这个例子中,我将温度设置为0.9,以使LLM更具创造力。它给出的答案是"MC MegaMatt"。我会给它9分(满分10分)。

### 聊天模型 

LLM模型生成说唱名字很有趣,但如果我们想要更复杂的答案和对话,就需要使用聊天模型,它比语言模型在技术上有所不同。用LangChain文档的话来说:

> 聊天模型是对语言模型的一种变体。虽然聊天模型在内部使用语言模型,但它们使用的接口有所不同。它们不是使用“输入文本,输出文本”的API,而是使用“聊天消息”作为输入和输出的接口。

以下是一个简单的Python聊天模型脚本:

```python
from langchain.llms import OpenAI
from langchain.chat_models import ChatOpenAI
from langchain.schema import (
    AIMessage,
    HumanMessage,
    SystemMessage
)
import os
os.environ["OPENAI_API_KEY"] = "YOUR_OPENAI_API_KEY"

chat = ChatOpenAI()
messages = [
    SystemMessage(content="你是一个友好、非正式的助手"),
    HumanMessage(content="说服我Djokovic比Federer更好")
]
print(chat(messages))
```

如上所示,代码首先发送了一个SystemMessage,告诉聊天机器人要友好和非正式,然后发送了一个HumanMessage,告诉聊天机器人说服我们Djokovic比Federer更好。

如果运行这个聊天机器人模型,你会看到类似下面的结果。

![](https://i.imgur.com/wywOYen.png)

### 嵌入模型

**嵌入(Embeddings)**是一种将文本块中的单词和数字转换为向量的方法,这些向量可以与其他单词或数字相关联。这听起来有点抽象,让我们来看一个示例:

```python
from langchain.embeddings import OpenAIEmbeddings

embeddings_model = OpenAIEmbeddings()
embedded_query = embeddings_model.embed_query("谁创造了万维网?") 
embedded_query[:5]
```

这将返回一个浮点数列表:[0.022762885317206383, -0.01276398915797472, 0.004815981723368168, -0.009435392916202545, 0.010824492201209068]。这就是嵌入的样子。

#### 嵌入模型的应用案例

如果我们想要训练一个聊天机器人或LLM来回答与数据或特定文本样本相关的问题,我们需要使用嵌入。让我们创建一个简单的CSV文件(embs.csv),其中包含一个包含三个信息的“text”列:

```
text
"Robert Wadlow是有史以来最高的人"  
"布尔嘉利发起是最高的摩天大楼"
"玫瑰是红色的"
```

现在,下面的脚本将根据问题“有史以来最高的人是谁?”从CSV文件中找到正确的答案,并将其格式化为JSON对象:

```python
from langchain.embeddings import OpenAIEmbeddings
from openai.embeddings_utils import cosine_similarity
import os
import pandas as pd

os.environ["OPENAI_API_KEY"] = "YOUR_OPENAI_KEY"
embeddings_model = OpenAIEmbeddings()

df = pd.read_csv("embs.csv")

# 对每个信息生成嵌入
emb1 = embeddings_model.embed_query(df["text"][0])  
emb2 = embeddings_model.embed_query(df["text"][1])
emb3 = embeddings_model.embed_query(df["text"][2])
emb_list = [emb1, emb2, emb3]
df["embedding"] = emb_list

embedded_question = embeddings_model.embed_query("有史以来最高的人是谁?") # 生成问题的嵌入
df["similarity"] = df.embedding.apply(lambda x: cosine_similarity(x, embedded_question)) # 找到每个数据片段与问题的相关性
df.to_csv("embs.csv")
df2 = df.sort_values("similarity", ascending=False) # 根据与问题的关联性对信息片段进行排序
print(df2["text"][0]) 
```

如果运行此代码,将会得到"Robert Wadlow是有史以来最高的人"作为输出。这段代码通过获取每个信息片段的嵌入并找到与问题"有史以来最高的人是谁?"嵌入最相关的那个来找到正确的答案。嵌入的威力!

## 分块

LangChain模型无法一次处理大量文本并生成响应。这就是分块和文本分割的作用。让我们看看两种将文本数据分割为块的简单方法。

### 按字符分块

为了避免分块时出现突然的中断,我们可以通过在每个换行符或双换行符处分割文本来按段落拆分文本:

```python
from langchain.text_splitter import RecursiveCharacterTextSplitter
text_splitter = RecursiveCharacterTextSplitter(separators=["\n\n", "\n"], chunk_size=2000, chunk_overlap=250)
texts = text_splitter.split_text(your_text)
```

### 递归分割块

如果我们想要严格按字符长度拆分文本,可以使用RecursiveCharacterTextSplitter:

```python
from langchain.text_splitter import RecursiveCharacterTextSplitter
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=2000,
    chunk_overlap=250, 
    length_function=len,
    add_start_index=True,
)
texts = text_splitter.create_documents([your_text])
```

#### 块大小和重叠

在查看上面的示例时,您可能想知道块大小和重叠参数的确切含义以及对性能的影响。可以通过以下两点来解释:

- 块大小决定了每个块中的字符数量。块大小越大,块中的数据越多,LangChain处理块的时间和生成输出的时间就越长,反之亦然。

- 块重叠是用于在块之间共享信息的机制,以便它们共享一些上下文。块重叠越高,块之间的冗余就越多;块重叠越低,块之间共享的上下文就越少。通常,良好的块重叠率在块大小的10%到20%之间,尽管理想的块重叠率因不同的文本类型和用例而异。

## 链

链基本上是将多个LLM功能链接在一起,以执行无法通过简单的LLM“输入->输出”方式完成的更复杂任务。让我们看一个有趣的示例:

```python
from langchain.llms import OpenAI
from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain
import os
os.environ["OPENAI_API_KEY"] = "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"

llm = OpenAI(temperature=0.9)
prompt = PromptTemplate(
    input_variables=["media", "topic"],
    template="为{media}关于{topic}制作一个好标题",
)
chain = LLMChain(llm=llm, prompt=prompt)
print(chain.run({
    'media': "恐怖电影",
    'topic': "数学"  
}))
```

这段代码接受两个变量作为其提示,并根据创造性的答案(temperature=0.9)进行格式化。在这个例子中,我们要求它为一部关于数学的恐怖电影想一个好标题。运行此代码后的输出是"The Calculating Curse",但这并不能完全展示链的强大之处。


让我们看一个更实际的例子:

```python
from langchain.chat_models import ChatOpenAI
from langchain.prompts import PromptTemplate
from typing import Optional

from langchain.chains.openai_functions import (
    create_openai_fn_chain,
    create_structured_output_chain,
)
import os

os.environ["OPENAI_API_KEY"] = "YOUR_KEY"

llm = ChatOpenAI(model="gpt-3.5-turbo", temperature=0.1)
template = """按照给定的格式从以下输入中提取信息:{input}。确保以正确的格式回答"""
prompt = PromptTemplate(template=template, input_variables=["input"])

json_schema = {
    "type": "object",
    "properties": {
        "name": {"title": "Name", "description": "The artist's name", "type": "string"},
        "genre": {"title": "Genre", "description": "The artist's music genre", "type": "string"}, 
        "debut": {"title": "Debut", "description": "The artist's debut album", "type": "string"},
        "debut_year": {"title": "Debut_year", "description":
        ```python
        "Year of artist's debut album", "type": "integer"}
    },
    "required": ["name", "genre", "debut", "debut_year"], 
}

chain = create_structured_output_chain(json_schema, llm, prompt, verbose=False)
f = open("Nas.txt", "r")
artist_info = str(f.read())
print(chain.run(artist_info))
```

这段代码读取一篇关于Nas(嘻哈艺术家)的短传记,并从文本中提取以下值,并将它们格式化为JSON对象:

- 艺术家的名字
- 艺术家的音乐风格
- 艺术家的首张专辑  
- 艺术家的首张专辑发行年份

在提示中,我们还指定“确保以正确的格式回答”,以便始终以JSON格式获取输出。这是该代码的输出:

```json
{'name': 'Nas', 'genre': 'Hip Hop', 'debut': 'Illmatic', 'debut_year': 1994}
```

通过向create_structured_output_chain函数提供JSON模式,我们使链将其输出放入JSON格式中。

## 超越OpenAI

即使我一直在使用OpenAI模型作为LangChain各种功能的示例,但LangChain并不限于OpenAI模型。我们可以将LangChain与许多其他LLM和AI服务集成(这是一个完整的可集成的LLM列表)。

例如,我们可以将LangChain与Cohere一起使用。在安装Cohere(pip3 install cohere)后,我们可以使用LangChain和Cohere编写一个简单的“问题->答案”的代码,如下所示:

```python
from langchain.llms import Cohere
from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain

template = """问题:{question}

答案:让我们一步一步地思考。"""
prompt = PromptTemplate(template=template, input_variables=["question"])
llm = Cohere(cohere_api_key="YOUR_COHERE_KEY")
llm_chain = LLMChain(prompt=prompt, llm=llm)

question = "Novak Djokovic是在哪一天出生的?"

print(llm_chain.run(question))
```

上面的代码输出如下:

```
The answer is Novak Djokovic was born on May 22, 1987. 

Novak Djokovic is a Serbian tennis player.
```

## 结论

在本指南中,您已经了解了LangChain的不同方面和功能。掌握了这些知识,您现在可以利用LangChain在NLP领域进行研究、开发或爱好项目。无论是研究人员、开发人员还是爱好者,都可以利用LangChain的能力。祝您在Python中使用LangChain进行愉快的编码和实验!
