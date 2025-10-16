# **MODULE 1**

## **VIDEO 1- Motivation**

A solitary language model is fairly limited because it doesn't have access to multi-step workflows. Which is why a lot of LLM applications use a control flow with steps before and after LLM calls, like including tool calls, retrieval calls etc.

The control flow is called a chain. An Agent then, is a control flow thats actually defined by the LLM. Its flexible and the LLM chooses what steps to take depending on the problem or situation faced instead of a procedural step-by-step fixed routine.

There are many kinds of Agents. A router is an agent that controls a single step in the flow. A fully autonomous agent can pick any sequence of steps. It can also generate its own step. A drawback is that the applications reliability decreases inversely with more control given to the LLM.

Langgraph gives you a way to implement custom control flows in the form of graphs with nodes connected by edges.

There was no code for this video.

---

## **VIDEO 2- Simple Graph**

[simple-graphVID2MOD1.ipynb](./simple-graphVID2MOD1)


In this video, we built a simple graph with 3 nodes and 1 conditional edge. The first node has a conditional edge that either goes to node 2 or node 3.

There are some concepts defined. A state is the object that we pass between the node and the edge. A node is basically a python function. We pass the state to the node. Each new node returns the new value of the state key and overrides the previous value. Edges connect the nodes.  

In this file, I've made a change so that the program checks the current date-time and if its before evening routes to saying that its awake, and if its post evening then states that its sleepy. We construct a graph by defining a START node and an END node, before we invoke it.






construct a graph by defining a START node and an END node, before we invoke it.


