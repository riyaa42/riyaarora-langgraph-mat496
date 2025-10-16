# **MODULE 1**

## **VIDEO 1- Motivation**

A solitary language model is fairly limited because it doesn't have access to multi-step workflows. Which is why a lot of LLM applications use a control flow with steps before and after LLM calls, like including tool calls, retrieval calls etc.

The control flow is called a chain. An Agent then, is a control flow thats actually defined by the LLM. Its flexible and the LLM chooses what steps to take depending on the problem or situation faced instead of a procedural step-by-step fixed routine.

There are many kinds of Agents. A router is an agent that controls a single step in the flow. A fully autonomous agent can pick any sequence of steps. It can also generate its own step. A drawback is that the applications reliability decreases inversely with more control given to the LLM.

Langgraph gives you a way to implement custom control flows in the form of graphs with nodes connected by edges.

There was no code for this video.

---

## **VIDEO 2- Simple Graph**

[simple-graphVID2MOD1.ipynb](./Module1/simple-graphVID2MOD1.ipynb)


In this video, we built a simple graph with 3 nodes and 1 conditional edge. The first node has a conditional edge that either goes to node 2 or node 3.

There are some concepts defined. A state is the object that we pass between the node and the edge. A node is basically a python function. We pass the state to the node. Each new node returns the new value of the state key and overrides the previous value. Edges connect the nodes.  

In this file, I've made a change so that the program checks the current date-time and if its before evening routes to saying that its awake, and if its post evening then states that its sleepy. We construct a graph by defining a START node and an END node, before we invoke it.

---

## **VIDEO 4- Chain**

[chainVID4MOD1.ipynb](./Module1/chainVID4MOD1.ipynb)

In this video, we see how to build a chain integrating chat messages, chat models and tool calls.
Langchain has different message types that are used to capture different roles in conversations. I have used gemini instead of OpenAI and have configured my code according to that. I learnt how to pass messages as inputs to chat models, and how to bind tools to chat models, and how to produce tool called outputs. I've learnt that we can use messages in our graph state.

We don't want messages to be overwritten in the state, instead we want them to append to the state so as to maintain message history. For this, we use reducers. Reducers allow us to specify how we want state updates to happen instead of just overriding. 

We've built a graph with MessageState and tool calling. For this module, I added on to the multipying tool and added division, addition, and subtraction tools as well. Other than that, I added a tool to tell current date-time, as well as a tool that tells the weather in a specified location that the user mentions. I have also changed the messages passed to the state. 

---

## **VIDEO 5- Router**

[routerVID5MOD1.ipynb](./Module1/routerVID5MOD1.ipynb)

We've seen that a graph can return either a tool call or a natural language response This is a router where a chat model routes between either a direct response or a tool call based on user input. Now I've extend the previous learnings in the file to add a node that calls the tool itself. I've also added a conditional edge that will look at the chat model output and rooute to our tool calling node or end if no tool call is performed.

We can now see the actual output when our tools are used, I've used the tools I defined myself before and I can now see the outputted temperature in New York through the tool call of the weather tool and the current date-time through the tool call of the date-time tool, as well as the results from all the arithmetic functions.










