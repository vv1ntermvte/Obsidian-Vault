
Titel: Comparison of Approaches for Knowledge Graph-Based Reasoning in LLMs: A Caste Study of LightPROF and Paths-over-Graph

LightPROF and Paths over Graph are two concepts for empowering the capabilities of LLMs by utilizing knowledge graphs. In my paper I want to address the core differences of the two methods, the similarities they share and in which way they are improving on the output LLMs generate. The paper will be divided into the following sections:

1. Abstract: Short summary of the paper (comes last)
2. Introduction: first I will address the general problem that arises with the use of LLMs. The core functionality many people are using them for in their everyday life is for knowledge acquisition. Humans are providing the LLM with a problem they require and expect a concrete answer to. This is a problem, because LLMs inherently lack the skill of providing factual knowledge. Instead they tend to hallucinate, providing answers that seem plausible but lack any meaningful logical basis. Utilizing knowledge graphs is one popular way to tackle this problem. -> What are knowledge graphs, why can they provide a factual knowledge basis. In this paper, two different methods of utilizing knowledge graphs within LLMs will be introduced, that were both developed with different goals in minds, leading to different strengths and weaknesses. These will be assessed and compared, which may either conclude in one being generally superior to the other or both excelling in different fields. 
3. Preliminaries: What are knowledge graphs, why are they necessary if one wants to improve the fact-fullness of LLMs, why do LLMs tend to hallucinate, what is Knowledge Graph Question Answering'
4. Main Chapter 1: [[1 - RoughNotes/LightPROF]]
   this Chapter will provide a summary of the methods the LightPROF approach utilizes.
5. Main Chapter 2: [[1 - RoughNotes/Paths over Graph]]
   this Chapter will provide a summary of the methods the Paths over Graph approach utilizes.
6. Main Chapter 3: Comparative Discussion
   this Chapter will include the results achieved with both approaches, summarize the similarities and differences between them and contextualize them with some own thoughts on how they might compete with each other in different scenarios and use cases
7. Conclusion: Summary of the knowledge gained in the previous chapters, especially 4, 5 and 6. This will be important for finishing the Introduction and writing the abstract.

Relevant sources:

(1) Roadmap for the unification of Large Language Models and Knowledge Graphs. Might has relevant information regarding the lacking of LLMs in factual knowledge (why knowledge graphs are promising)
https://ieeexplore.ieee.org/document/10387715

(7) Think on Graph. Info about the struggle with deep and responsible reasoning
https://www.researchgate.net/publication/372416758_Think-on-Graph_Deep_and_Responsible_Reasoning_of_Large_Language_Model_with_Knowledge_Graph

(4) Graph of thoughts. Info about LLM performance in various tasks
https://dl.acm.org/doi/10.1609/aaai.v38i16.29720

(3) Chain of thought
https://dl.acm.org/doi/10.5555/3600270.3602070

(2) language models are few shot learners 
https://dl.acm.org/doi/abs/10.5555/3495724.3495883

(5) Paths over Graph

(6) MindMap: Knowledge Graph Prompting Sparks Graph of Thoughts
https://aclanthology.org/2024.acl-long.558/

(8) LightPROF




Abstract: This paper presents different existing methods of utilizing knowledge graphs on Large Language Models, in order to incorporate external knowledge into a models reasoning process, resulting in higher reliability and quality of results. Specifically, two state of the art frameworks are analyzed: Paths over Graph and LightPROF. Featuring different approaches, Paths over Graph focues on ... , while LightPROF ... ,. Both methods are subsequently compared with each other, leading to the conclusion, that ... , while ... . 

Keywords: Knowledge Graph, Large Language Models, 

Introduction: Within recent years, Large Language Models (LLMs) have been able to produce impressive results in a multitute of different tasks in natural language processing, ranging from basic question answering to translation and text generation tasks [1]. This could be elevated through various measures, specifically tremendous amounts of pre-training, scaling up model size and applying prompt engineering techniques to elicit the LLMs internal knowledge, which have shown to improve LLM performance drastically, even on more complex tasks [2, 3, 4]. Despite these measures taken, LLMs still have severe flaws in certain fields, especially when it comes to providing reliable knowledge. Two drawbacks LLMs keep struggling with, despite the established improvements, are hallucinations and a lack transparency. For one, the internal knowledge of LLMs requires extensive and regular (re-)training, for  the provided knowledge to stay relevant as well as reasoning being accurate, which is high in cost and makes them prone to errors due to outdated or missing knowledge. Secondly, the black-box character of LLMs causes the knowledge interpretation to be entirely concealed, making proper validation of the reasoning process impossible [5, 6].

To improve upon these issues, especially when facing complex knowledge intensive tasks that require deep and responsible reasoning, the incorporation of Knowledge Graphs (KGs) into the reasoning process of LLMs has shown to be a very promising approach [7]. KGs offer an extensive source of rich, factual knowledge, that can be leveraged as a reliable external knowledge base for accessible, accurate and relevant information, thus improving the capabilities of LLMs significantly [1, 8]. There are different approaches to complementing LLM reasoning with the usage of KGs, of which the integration is usually assessed using Knowledge Graph Question Answering (KGQA), a knowledge requiring task, during which knowledge obtained from the KG is utilized to answer a set of KG specific questions. However, despite the improvements achieved through the utilization of KGs, several challenges remain. Previous methods like Think-on-Graph (ToG) usually employ an individual exploration of each of a questions topic entities. To achieve adequate results, two factors must be regarded; For more complex questions, that require the utilization of multi-hop reasoning, simply observing the one-hop neighbors of a entity will not be sufficient, leading to erroneous answers. Instead, a multi-hop neighborhood must be examined. In Addition, as the topic entities are explored separately, the exploration of the KG for such multi-entity questions can lead to significant computational effort and inadequate results, due to much superfluous information being gathered [5]. In Consequence, this necessitates a bigger context window to prompt the KG to the LLM, subsequently leading to loss of context if the LLMs power didn't suffice or even hallucination from redundant information. Moreover, current methods often miss out on utilizing the graph structure immanent to KGs, instead converting the collected knowledge into a textual format, like multidimensional lists or even natural language, which is then prompted to the LLM, but without properly conveying the structural information and logical relationships of the KG in all their complexity [8].  

Two recent methods, that try to adress these challenges, are LightPROF and Paths-over-Graph (PoG), which will be introduced in the following chapters in more detail.

current state of the art:
LightPROF:
- retrieving information from KGs and incroporating the results into LLM input prompts. 
- several remaining challenges: KG content often represented as textual content, fails to convey logical relationships of the graph structure, which are crucial for reasoning
- in previous work presented as multidimensional lists or in natural language form, making expression of complex relationships and hierarchical structures difficult
- retrieval and reasoning on KG demand a high number of LLLM calls + substantial reasoning power. Previous work used iterative approaches starting from the entity and obtaining information step by step. This increased the number of LLM calls, sacrificing reasoning efficiency and feasibility and produces redundant information
- Because the textual content is so vast, a large context window is required, meaning a powerful LLM is needed to ensure that no information is missed.
- natural language form exposes risk of redundant content
Paths over Graph:
- current metods (ToG) explore from each topic entity, LLM selects knowledge tripples. Process relies on LLMs inherent understanding of the triples, for multi hop reasoning this introduces significant computational overhead
- with topic entities explored independently, interconnections are not considered resulting in large amounts of irrelevant information. 
- inherent graph structure is often overlooked (MindMap)
