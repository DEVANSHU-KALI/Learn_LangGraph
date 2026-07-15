# LangGraph
**Technically**, langgraph is a framework, which provides you multiple inbuilt libraries to build an AI agent. where the code looks more cleaner and simple to write.

But in simple terms, here is how you can understand that with a simple example:

**langgraph is like a manager of an office filled with AI workers.**

If you have a standard AI (like chatgpt), its like having a smart employee. you give a task to it, it thinks about the task and give you some response. But what if you got a massive project that requires research, writing, some problem solving, checking whether the work done is correct or not, one employee can't handle all that. 

here comes the langgraph, helping you to set up the entire office of workers. And it provides you lot of things:
- You have **STATE** (a shared clipboard): Imagine a clipboard that gets passed around the office, holding the current status of the project in a very detailed form.
- Next **NODES** (the workers): you create workers for specific tasks. Each working on some task.
- Then **EDGES** (the flow rule): langgraph acts as manager deciding who gets that clipboard next based on some set of rules. "for example: if researcher finishes a draft, next the draft is sent to writer, each and every time. 

- These are the main block which helps to get started, but there are more sub concepts which provide more control over your system.

### Now lets get a real example:
- lets say you want to build a RAG system combined with langgraph. 
    - where you pass a query and get some response, with multiple sub works getting done before the response arrives. 
    - lets say you have ***Researcher node*** which has access to your local data and also the internet. 
    - following up with ***Writer node*** which takes that raw response of researcher node and structures the response.
    - next a ***Reviewer node*** which fact checks the result. 
        - if everything is correct, set that response as the final answer
        - if not, this reviewer node will provide some feedback to the writer node and let the writer node generate some new answer again until the reviewer node gets satisfied.
        - you can customize how many times you want that loop, where this reviewer node give some feedback and writer node generates a new answer. 

    - If needed you can also interrupt the flow at any node to check whatever you want, lets say you want to see the writer node's response before the system directly jumps to the reviewer node. which is called ***Human In The Loop***, you can also do this.

### Now, one of the main doubt, can't we build a systems like this without langgraph?
- You can!!. But you may feel like you got spawned in hard core mode. let me tell you why!:
    - let's say you somehow built the nodes, which are just some smaller functions (worker). where did you coded that logic?. In a separate python file mostly. 
    - Then you try to write the logic for the connection between these functions, and that's where it becomes hard. you need to write long codes which connects all these components.
    - Lets assume for a second that, you got all the logic for connecting the nodes.
        - But what if you want to see the updates happening to each state.
        - What if you want to loop between nodes? (e.g., A worker writes a draft, the critic rejects it, and it goes back to the worker). Writing custom, infinite while loops that safely manage state is a nightmare.
        - what if you want loop between the nodes
        - there are more which makes the hard coding unreliable.

--- 

### Additionally, lets get some knowledge about langchain first, for the users who dont have any knowledge about ai world and langchain which came first before langgraph and for users who want to know why langgraph if we had langchain.

**The Golder era of langchain**. where it was unbeatable in AI development.
- Before we talk about LangGraph, we should have lots of respect to standard LangChain. Before LangGraph even existed, LangChain was the absolute undisputed king of AI development. 
- LangChain completely revolutionized this by introducing LCEL (LangChain Expression Language).
-  LCEL allowed developers to chain different AI components together using a simple pipe operator (|), just like an assembly line.
- A Small Example of LCEL's Brilliance:

```python 
# Instead of writing 20 lines of complex API calls, 
# LangChain let developers do this:
chain = prompt | llm | output_parser
result = chain.invoke({"question": "What is AI?"})
```

Why was this revolutionary at the time?
This incredibly simple syntax was top-notch because the "|" operator did a massive amount of heavy lifting behind the scenes. By just putting a | between components, LangChain automatically knew how to stream responses word-by-word, run multiple queries asynchronously, and pass data perfectly from one step to the next. It turned complex AI engineering into clean, readable Lego blocks.

Beyond LCEL: A Massive Ecosystem
- But it wasn't just this expression language that made LangChain great; there were a lot of other features that were incredibly useful at that point. LangChain provided a massive ecosystem of built-in utilities right out of the box. From Document Loaders that could instantly read PDFs and scrape websites, to Text Splitters that perfectly chunked data, to hundreds of pre-built integrations with vector databases and third-party APIs. It gave developers a complete AI utility belt so they didn't have to reinvent the wheel for every new project. Even I used langchain a lot in my project related to RAG applications and chat bots.

The Turning Point:
LCEL and this massive ecosystem are still the absolute best ways to build a straight-line, sequential pipeline. But as AI evolved, developers realized they didn't just want an "assembly line"—they wanted autonomous "Agents."

Because the LCEL pipe (|) only pushes data forward, it creates a strict one-way street (a DAG, or Directed Acyclic Graph). When your AI needs to pause, use a tool, realize it made a mistake, and loop backward to try again, the | operator simply wasn't designed for it.

That is exactly where LangGraph stepped in: it kept the brilliant Lego blocks and utility belt of LangChain, but gave them a massive upgrade so they could loop, remember, and self-correct.

> note: You don't have to throw away your LangChain knowledge. LangGraph is simply the upgrade that takes your LangChain components and organizes them into a stateful, looping, multi-agent office.

---

### I'll also provide another repo including a "Research Agent" project combining these concepts. So that the learning will be totally different from that project. 