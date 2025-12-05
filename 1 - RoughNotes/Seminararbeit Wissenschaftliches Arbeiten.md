
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

Roadmap for the unification of Large Language Models and Knowledge Graphs. Might has relevant information regarding the lacking of LLMs in factual knowledge (why knowledge graphs are promising)
https://ieeexplore.ieee.org/document/10387715

Think on Graph. Info about the struggle with deep and responsible reasoning
https://www.researchgate.net/publication/372416758_Think-on-Graph_Deep_and_Responsible_Reasoning_of_Large_Language_Model_with_Knowledge_Graph

(4) Graph of thoughts. Info about LLM performance in various tasks
https://dl.acm.org/doi/10.1609/aaai.v38i16.29720

(3) Chain of thought
https://dl.acm.org/doi/10.5555/3600270.3602070

(2) language models are few shot learners 
https://dl.acm.org/doi/abs/10.5555/3495724.3495883

Abstract: This paper presents different existing methods of utilizing knowledge graphs on Large Language Models, in order to incorporate external knowledge into a models reasoning process, resulting in higher reliability and quality of results. Specifically, two state of the art frameworks are analyzed: Paths over Graph and LightPROF. Featuring different approaches, Paths over Graph focues on ... , while LightPROF ... ,. Both methods are subsequently compared with each other, leading to the conclusion, that ... , while ... . 

Introduction: Within recent years, Large Language Models (LLMs) have been able to produce impressive results in a multitute of different tasks ranging from reading comprehension to ... [1] . This could be achieved through various measures, specifically scaling up model size to increase overall LLM efficiency [2] and applying prompt engineering techniques, such as chain-of-thought (CoT) or Graph of Thoughts (GoT), which have shown to improve LLM performance drastically, even on more complex tasks [3, 4]. Despite these measures taken, LLMs still have severe flaws in certain fields, especially when it comes to providing reliable knowledge. One drawback LLMs keep struggling with despite the established improvements, is hallucination. 