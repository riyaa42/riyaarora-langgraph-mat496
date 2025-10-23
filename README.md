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

## **VIDEO 3- Langgraph Studio**

We learnt how to utilize langgraph studio, which is an IDE for building, visualizing, and debugging AI agent workflows made with LangGraph. We can see visual graphs with all the nodes and see how they process inputs/outputs more clearly. We need a studio folder in our directory that has a langgraph.json file in it which has the graphs that we want to see and our .env file. I made a copy of my jupyter notebook .ipynb file into .py files to save in the studio folder in my directory and then ran the command to view langgraph studio. We can see what each node does and which node is running real time in the studio.

<img width="1768" height="907" alt="image" src="https://github.com/user-attachments/assets/5ac32ca2-e0b2-468a-95ff-673a16bbd142" />

There is no code in this video so i just interacted with langgraph studio. Here in the image you can see at my input of the GraphState the output gives me the line "I am sleepy" this is because my code in the relevant simple-graph file, at node 1 the program checks the current date-time of the system and if it is after evening it routes it to the node to say the phrase "I am sleepy". In my jupyter notebook file you can see when I ran the code intitially the graph gave "I am awake" as it was before 6pm.

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

<img width="1743" height="931" alt="image" src="https://github.com/user-attachments/assets/4ae5dfb1-0ee1-464a-95d6-c9d21a7af668" />
In this image we have utilized Langgraph studio to see the graph. Here we can also input messages and see the result of the tool calling LLM, where it chooses which tool to call to give the correct output. Here you can see the outputs from calling the tools to see current date-time and the weather in a user specified location. These are custom tools that I made. 

<img width="1807" height="918" alt="image" src="https://github.com/user-attachments/assets/f8123573-902c-44fd-b008-d538f8fa267e" />
In this image you can see 2 of the arithemetic tools I defined. I also defined seperate tools for addition and subtraction as seen in the jupyter notebook file.


---

## **VIDEO 6- Agent**

[agentVID6MOD1.ipynb](./Module1/agentVID6MOD1.ipynb)

We can make simple modifications to the router to turn it into popular agent architecture, ReAct. The model calls specific tools as previously seen, and now the tool output is passed back to the model. The model then decides what to do next with the tool output ( call another tool or respond directly). 

I have first defined all the tools I previously used, basic arithemetic (addition, subtraction, multiplication, division) and the environmental variable tools (current date, current time, fetching weather of specific location). I have also added more arithemtic tools (square of input, root of input, and modulo). I have attatched screenshots of the tracing on langsmith for 2 queries I ran, one was a series of arithemetic operations and the other was a series of requests about date/time/weather. Langsmith tracing showcases the multiple tool calls before the output.

---

## **VIDEO 7- Agent Memory**

[agent-memoryVID7MOD1.ipynb](./Module1/agent-memoryVID7MOD1.ipynb)

In this section, I learnt how to extend the previous agent architecture to include memory. We run the previous agent and try to ask a follow up arithemetic question on the output of the previous result. This doesn't work because there is no memory saved of previous outputs. There is no persistence between executions.

Langchain uses checkpointers to save the GraphState after each step. We use the MemorySaver checkpointer, which is an in-memory key-value store for GraphState. We compile the graph with the checkpointer, which gives memory to the graph. I have used the agent I established in the previous file and demonstrated that the agent retains memory and can call tools and perform the arithmetic functions on a previous output given by the agent that it remembers. 

<img width="1755" height="930" alt="image" src="https://github.com/user-attachments/assets/82f4345f-31f7-483e-86ae-f0668da36c7b" />
<img width="1808" height="926" alt="image" src="https://github.com/user-attachments/assets/ce75e546-c9fa-4adf-95f7-cccbd0088ea3" />


Here we can see it in langgraph studio where we input a question that calls some tools that I have defined and gives an output, then we ask it to do further operations on the previous output and it is able to do that with its memory.

---

# **MODULE 2**

## **VIDEO 2- State Schema**

[state-schema.ipynb](./Module2/state-schema.ipynb)

In module one, we've covered how to make oan agent with memory that can use tools and can decide what to do next based on tool call outputs. In this video, we extend about this and go deeper into the state.  When defining a langgraph StateGraph, you use aa state schema, which comprimises of the structure and the type of data the graph will use. We have previously been using TypeDict which is a dictionary with type hints as keys that are not enforcable in runtime. 

We use TypeDict first where I have *changed*:

- Defined a 2 level decision tree with several nodes based on selecting a genre of book to read + time taken to read, the decison tree first randomly selects a node out of 3 nodes for book genres (horror, fantasy, sci-fi) and then theres 2 more nodes that are connected individually to all three of these nodes that define a short reading time or a long reading time. 

Now I have used dataclass and pydantic to define the same graph that I have modified with more nodes and branches. DataClass, used to define a class of structured data, also does not enforce type hints at runtime, which is why we use Pydantic when we want data validation.

---

## **VIDEO 2- State Reducers**

[state-reducers.ipynb](./Module2/state-reducers.ipynb)

In this video we learn about state reducers which specify how state updates are performed on specific keys or channels in the schema. Whenever we invoke a graph, langgraph doesn't know the preffered way to update the state, so the default method is to override the value from before. We see this in an example of a branching graph where the key can only recieve one value per step, but since parallel processes are trying to occur and overwrite the value at the same time, an error occurs.

This is why we use Annotated key to handle multiple values. We apply the annotated type to our key and include a reducer function, which performs a list concatenation instead of overwriting. So when 2 processes occur at once, they are not trying to overwrite at the same time but just append, this is useful for performing state updates simultaneously.

We've also learnt to define custom reducers to handle specific inputs like edge cases (null value here)

We also learn more about MessagesState and defining a custom one, add_messages is a built in reducer.

The changes I have made are changing the key from foo to book_title which is a string. The rest of the code is modified to show the functionality of reducers using string and not int. The graph nodes are defined to be about tracking books and genres in a library, and the reducers show the book list being appended. The messafesstate section is modified to include a thread of conversation about book reccomendation.






