
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


Abstract: This paper presents different existing methods of utilizing knowledge graphs on Large Language Models, in order to incorporate external knowledge into a model's reasoning process, resulting in higher reliability and quality of results. Specifically, two state-of-the-art frameworks are analyzed: LightPROF and Paths-over-Graph. Featuring different approaches, LightPROF focuses on an adapter-based approach, mapping the information gathered from a knowledge graph into the embedding space of the LLM, resulting in superb knowledge interpretability, while Paths-over-Graph involves thorough path exploration and pruning strategies, utilizing the performance of the LLM itself to maximize the relevance of the retrieved knowledge. Subsequently the distinct deployment niches for each framework based on their inherent differences are identified, resulting in the assessment, that Paths-over-Graph offers universal applicability across both closed and open-source systems, though it necessitates high-power models to acquire the textual representation of KG knowledge. Conversely, LightPROF is identified as the more computationally efficient solution, yet it remains exclusive to open-source architectures due to its requirement for direct embedding space access.

Keywords: Knowledge Graph, Large Language Models, 

Introduction: Within recent years, Large Language Models (LLMs) have been able to produce impressive results in a multitute of different tasks in natural language processing, ranging from basic question answering to translation and text generation tasks [1]. This could be elevated through various measures, specifically tremendous amounts of pre-training, scaling up model size and applying prompt engineering techniques to elicit the LLMs internal knowledge, which have shown to improve LLM performance drastically, even on more complex tasks [2, 3, 4]. Despite these measures taken, LLMs still have severe flaws in certain fields, especially when it comes to providing reliable knowledge. Two drawbacks LLMs keep struggling with, despite the established improvements, are hallucinations and a lack transparency. For one, the internal knowledge of LLMs requires extensive and regular (re-)training, for  the provided knowledge to stay relevant as well as reasoning being accurate, which is high in cost and makes them prone to errors due to outdated or missing knowledge. Secondly, the black-box character of LLMs causes the knowledge interpretation to be entirely concealed, making proper validation of the reasoning process impossible [5, 6].

To improve upon these issues, especially when facing complex knowledge intensive tasks that require deep and responsible reasoning, the incorporation of Knowledge Graphs (KGs) into the reasoning process of LLMs has shown to be a very promising approach [7]. KGs offer an extensive source of rich, factual knowledge, that can be leveraged as a reliable external knowledge base for accessible, accurate and relevant information, thus improving the capabilities of LLMs significantly [1, 8]. There are different approaches to complementing LLM reasoning with the usage of KGs, of which the integration is usually assessed using Knowledge Graph Question Answering (KGQA), a knowledge requiring task, during which knowledge obtained from the KG is utilized to answer a set of KG specific questions. However, despite the improvements achieved through the utilization of KGs, several challenges remain. Previous methods like Think-on-Graph (ToG) usually employ an individual exploration of each of a questions topic entities. To achieve adequate results, two factors must be regarded; For more complex questions, that require the utilization of multi-hop reasoning, simply observing the one-hop neighbors of a entity will not be sufficient, leading to erroneous answers. Instead, a multi-hop neighborhood must be examined. In Addition, as the topic entities are explored separately, the exploration of the KG for such multi-entity questions can lead to significant computational effort and inadequate results, due to much superfluous information being gathered [5]. In Consequence, this necessitates a bigger context window to prompt the KG to the LLM, subsequently leading to loss of context if the LLMs power didn't suffice or even hallucination from redundant information. Moreover, current methods often miss out on utilizing the graph structure immanent to KGs, instead converting the collected knowledge into a textual format, like multidimensional lists or even natural language, which is then prompted to the LLM, but without properly conveying the structural information and logical relationships of the KG in all their complexity [8].  

Two recent methods, that try to adress these challenges, are LightPROF and Paths-over-Graph (PoG). LightPROF is a novel lightweight reasoning framework that adopts a "Retrieve-Embed-Reason" paradigm to empower small-scale LLMs with stable retrieval and efficient reasoning capabilities. Addressing the inefficiencies of converting KGs into raw text, LightPROF utilizes a specialized Transformer-based Knowledge Adapter. This component accurately retrieves relevant reasoning graphs based on relational semantics and subsequently fuses both the factual text and the complex structural information into compact "soft prompts". By mapping these dense vector representations directly into the LLM's token space, the framework significantly reduces input token redundancy and resource consumption. This allows for the effective injection of external knowledge into small-scale, open-source LLMs, enabling them to tackle complex multi-hop questions without the need for extensive parameter updates or massive computational overhead [8]. 

Similar to LightPROF, PoG is a framework enhancing LLM reasoning by integrating structured knowledge reasoning paths from Knowledge Graphs rather than relying on isolated facts or disjointed triples. To effectively address complex multi-hop and multi-entity questions however, PoG employs a dynamic three-phase path exploration strategy guided by the LLM's own planning indicators. This process involves constructing a relevant question subgraph and exploring paths that sequentially connect topic entities, while also supplementing this data with LLM-generated insights where explicit graph connections may be missing. Crucially, the framework implements a robust pruning mechanism that filters these candidates using graph structural analysis and semantic similarity to remove irrelevant noise. By prompting the LLM to generate answers based on these finalized reasoning chains, PoG ensures that the resulting outputs are not only accurate but also fully interpretable and grounded in verifiable knowledge[5].

Related Work:
Prompt Engineering on LLMs

KG-based LLM Reasoning

Preliminaries:
Knowledge Graph

Comparative Discussion:
Comparing the two aforementioned frameworks, one can notice that the authors of both in part identified the same challenges, regarding the integration of KGs into LLMs, and utilized similar measurements to deal with them. Accordingly, LightPROF and PoG both recognize the problem of previous frameworks usually exploring the different topic entities independent from one another, and counteract this, by ... . Similarly, both acknowledge that previous works often times translated KGs into a textual format, that wasn't properly conceivable in its entirety by the LLM. However, LightPROF and PoG engage this difficulty in a fundamentally different manner. 

LightPROFs approach is to convert the semantic and structural information from the knowledge graph from a textual format into the embedding space of the LLM, making it as directly interpretable as possible and greatly reducing the share of redundant information. This also has the benefit of reducing the token count drastically, by up to 98%, leading to LightPROF excelling in efficiency. This in addition to the fact, that in the LightPROF model only the so called knowledge-adapter needs to be trained, in consequence means, that this framework has a tremendous benefit for small-scale LLMs and resource-constrained environments, where efficiency and a low operating cost are required. For the same reason however, LightPROF depends on open-source models that allow access to the embedding space, excluding closed-source models in advance. 

PoG follows an entirely different approach, effectively keeping a plain-text format at all times and only applying smart prompt-engineering, to convert the retrieved knowledge into a format, that preserves the structural and semantic information of the KG as much as possible. To achieve this, PoG makes use of the LLM itself for pruning and path-selection. This leads to no additional training being required and even yields the possibility of utilizing closed-source models. The trade-off, however, is higher computational cost during the exploration and the need for a much larger context window, meaning that PoG will only excel when used with large-scale LLMs.

Conclusion:
In conclusion, the integration of Knowledge Graphs into Large Language Models remains a critical avenue for overcoming the inherent limitations of LLMs regarding hallucinations and lack of transparency. The examination of LightPROF and Paths-over-Graph (PoG) highlights two distinct yet complementary philosophies in addressing the challenges of multi-hop reasoning and structural preservation. LightPROF offers a parameter-efficient solution by embedding structural knowledge directly into the soft prompt space, making it a highly effective framework for small-scale, open-source models where resource constraints are a priority \cite{b8}. Conversely, PoG leverages the advanced semantic planning capabilities of large-scale LLMs to navigate and prune graph paths in natural language, offering a robust zero-shot solution compatible with proprietary, closed-source architectures \cite{b5}.

Ultimately, the choice between these frameworks is dictated by the specific operational constraints of the application. LightPROF is the superior candidate for high-efficiency, training-accessible environments, whereas PoG excels in generalized, inference-heavy applications utilizing state-of-the-art proprietary models. Future research in this domain will likely focus on bridging this gap, potentially exploring hybrid architectures that combine the retrieval efficiency of embedding-based methods with the interpretive flexibility of path-based prompting.

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


LaTeX file:

\documentclass[conference]{IEEEtran}
\IEEEoverridecommandlockouts
% The preceding line is only needed to identify funding in the first footnote. If that is unneeded, please comment it out.
\usepackage{cite}
\usepackage{amsmath,amssymb,amsfonts}
\usepackage{algorithmic}
\usepackage{graphicx}
\usepackage{textcomp}
\usepackage{xcolor}
\usepackage{caption}
\captionsetup[figure]{skip=5pt}

\def\BibTeX{{\rm B\kern-.05em{\sc i\kern-.025em b}\kern-.08em
    T\kern-.1667em\lower.7ex\hbox{E}\kern-.125emX}}
\begin{document}

\title{Comparison of Approaches for Knowledge Graph-Based Reasoning in LLMs\\
{\large A Case Study of LightPROF and Paths-over-Graph}
}

\author{\IEEEauthorblockN{Luis Kolvenbach}
\IEEEauthorblockA{\textit{Technische Universität Wien}\\
Vienna, Austria \\
e12327946@student.tuwien.ac.at}
}

\maketitle

\begin{abstract}
Abstract: This paper presents different existing methods of utilizing knowledge graphs on Large Language Models, in order to incorporate external knowledge into a model's reasoning process, resulting in higher reliability and quality of results. Specifically, two state-of-the-art frameworks are analyzed: LightPROF and Paths-over-Graph. Featuring different approaches, LightPROF focuses on an adapter-based approach, mapping the information gathered from a knowledge graph into the embedding space of the LLM, resulting in superb knowledge interpretability, while Paths-over-Graph involves thorough path exploration and pruning strategies, utilizing the performance of the LLM itself to maximize the relevance of the retrieved knowledge. Subsequently the distinct deployment niches for each framework based on their inherent differences are identified, resulting in the assessment, that Paths-over-Graph offers universal applicability across both closed and open-source systems, though it necessitates high-power models to acquire the textual representation of KG knowledge. Conversely, LightPROF represents the more computationally efficient solution, yet it remains exclusive to open-source architectures due to its requirement for direct embedding space access.
\end{abstract}

\begin{IEEEkeywords}
Knowledge Graph, Large Language Models
\end{IEEEkeywords}

\section{Introduction}
Within recent years, Large Language Models (LLMs) have been able to produce impressive results in a multitute of different tasks in natural language processing, ranging from basic question answering to translation and text generation tasks \cite{b1}. This could be elevated through various measures, specifically tremendous amounts of pre-training, scaling up model size and applying prompt engineering techniques to elicit the LLMs internal knowledge, which have shown to improve LLM performance drastically, even on more complex tasks \cite{b2, b3, b4}. Despite these measures taken, LLMs still have severe flaws in certain fields, especially when it comes to providing reliable knowledge. Two drawbacks LLMs keep struggling with, despite the established improvements, are hallucinations and a lack transparency. For one, the internal knowledge of LLMs requires extensive and regular (re-)training, for  the provided knowledge to stay relevant as well as reasoning being accurate, which is high in cost and makes them prone to errors due to outdated or missing knowledge. Secondly, the black-box character of LLMs causes the knowledge interpretation to be entirely concealed, making proper validation of the reasoning process impossible \cite{b5, b6}.

To improve upon these issues, especially when facing complex knowledge intensive tasks that require deep and responsible reasoning, the incorporation of Knowledge Graphs (KGs) into the reasoning process of LLMs has shown to be a very promising approach \cite{b7}. KGs offer an extensive source of rich, factual knowledge, that can be leveraged as a reliable external knowledge base for accessible, accurate and relevant information, thus improving the capabilities of LLMs significantly [1, 8]. There are different approaches to complementing LLM reasoning with the usage of KGs, of which the integration is usually assessed using Knowledge Graph Question Answering (KGQA), a knowledge requiring task, during which knowledge obtained from the KG is utilized to answer a set of KG specific questions. However, despite the improvements achieved through the utilization of KGs, several challenges remain. Previous methods like Think-on-Graph (ToG) usually employ an individual exploration of each of a questions topic entities. To achieve adequate results, two factors must be regarded; For more complex questions, that require the utilization of multi-hop reasoning, simply observing the one-hop neighbors of a entity will not be sufficient, leading to erroneous answers. Instead, a multi-hop neighborhood must be examined. In Addition, as the topic entities are explored separately, the exploration of the KG for such multi-entity questions can lead to significant computational effort and inadequate results, due to much superfluous information being gathered [5]. In Consequence, this necessitates a bigger context window to prompt the KG to the LLM, subsequently leading to loss of context if the LLMs power didn't suffice or even hallucination from redundant information. Moreover, current methods often miss out on utilizing the graph structure immanent to KGs, instead converting the collected knowledge into a textual format, like multidimensional lists or even natural language, which is then prompted to the LLM, but without properly conveying the structural information and logical relationships of the KG in all their complexity \cite{b8}.  

Two recent methods, that try to adress these challenges, are LightPROF and Paths-over-Graph (PoG). LightPROF is a novel lightweight reasoning framework that adopts a "Retrieve-Embed-Reason" paradigm to empower small-scale LLMs with stable retrieval and efficient reasoning capabilities. Addressing the inefficiencies of converting KGs into raw text, LightPROF utilizes a specialized Transformer-based Knowledge Adapter. This component accurately retrieves relevant reasoning graphs based on relational semantics and subsequently fuses both the factual text and the complex structural information into compact "soft prompts". By mapping these dense vector representations directly into the LLM's token space, the framework significantly reduces input token redundancy and resource consumption. This allows for the effective injection of external knowledge into small-scale, open-source LLMs, enabling them to tackle complex multi-hop questions without the need for extensive parameter updates or massive computational overhead \cite{b8}. 

Similar to LightPROF, PoG is a framework enhancing LLM reasoning by integrating structured knowledge reasoning paths from Knowledge Graphs rather than relying on isolated facts or disjointed triples. To effectively address complex multi-hop and multi-entity questions however, PoG employs a dynamic three-phase path exploration strategy guided by the LLM's own planning indicators. This process involves constructing a relevant question subgraph and exploring paths that sequentially connect topic entities, while also supplementing this data with LLM-generated insights where explicit graph connections may be missing. Crucially, the framework implements a robust pruning mechanism that filters these candidates using graph structural analysis and semantic similarity to remove irrelevant noise. By prompting the LLM to generate answers based on these finalized reasoning chains, PoG ensures that the resulting outputs are not only accurate but also fully interpretable and grounded in verifiable knowledge \cite{b5}.

\section{Related Work}

\subsection{Prompt Engineering on LLMs}
blablabla

\subsection{KG-based LLM Reasoning}
blablabla

\section{Preliminaries}
Before you begin to format your paper, 

\section{LightPROF}
LightPROF is a framework that was recently introduced as a "Retrieve-Embed-Reason" approach to address some of the aforementioned challenges, specifically the high resource consumption of large-scale models and the loss of structural information when converting KGs to text. It is designed to empower small-scale Large Language Models (LLMs) with the ability to perform complex reasoning tasks by leveraging precise retrieval mechanisms and fine-grained structured data processing. As depicted in the framework's architecture, the process is divided into three distinct phases: Reasoning Graph Retrieval, Knowledge Embedding, and Knowledge Prompts Mixed Reasoning. These steps are also individually broken down in Fig. 1.

\begin{figure}[htbp]
\centerline{\includegraphics[width=0.5\textwidth]{lightprof_architecture.png}}
\caption{schematic depiction of the LightPROF framework \cite{b5}}
\label{fig}
\end{figure}

\subsection{Reasoning Graph Retrieval}
The framework starts with the retrieval of the concrete reasoning graph from the KG, which is paramount for complex multi-hop Question Answering tasks, as it determines how efficiently and accurately information is sourced from the KG. To optimize this proc, the retrieval module is further segmented into three specific steps: semantic extraction, relation retrieval, and reasoning graph sampling. Initially, the semantic extraction step focuses focuses on identifying the required semantic information contained in the KG, specifically the expected number of hops needed and the anchor entities, to narrow down the subsequent scope of the search without loosing out on essential data. For a given question, a pre-trained language model like BERT is fine-tuned to analyze the semantic vector of the query. This model learns to predict the specific number of hops $h_q$ required within the KG to adequately answer the question.

Following the determination of the necessary hop depth, the process moves to relation retrieval. Unlike entities, which can be complex and instable, relations in KGs offer a more durable and intuitive unit for retrieval, providing clear semantic connections between entities. To maximize the gathering of relevant knowledge, the model initiates a constrained breadth-first search (BFS) starting from identified anchor entities in the question. The previously predicted number of hops $h_q$ is now utilized as a bound for the depth of this search, ensuring that the system retrieves all relation links extending from the anchor entity up to the previously identified depth without unnecessary expansion. 

Subsequently, in the reasoning graph sampling step, these collected relation links are evaluated by an LLM, which applies scores based on how semantically relevant they are for answering the original question and ranks them accordingly. Based on the best-scoring links, the KG is sampled and a set of reasoning paths is selected, which together form the semantically enhanced reasoning graph $G_R$.

\subsection{Knowledge Embedding}
The second phase addresses the limitation that natural language descriptions of KGs often contain redundancy and fail to convey inherent structural patterns essential for deep understanding. To resolve this, a compact Transformer-based Knowledge Adapter is employed to encode the textual content of the reasoning graph into embeddings while simultaneously containing its structural information. 

The embedding process itself dual-faceted. The adapter operates by first decomposing the reasoning graph into individual reasoning paths, each consisting of a set of at most $h_q$ triples each of the form $(h,r,t)$. The embeddings for all three values are extracted by employing an embedding function using BERT, resulting in an embedding triple $(e^h,e^r,e^t)$, which is then further transformed to a structural embedding $s$, containing the local structural information of an entity-relation triple. Subsequently, all the structural embeddings of a given reasoning path are aggregated to form the structural embedding $z^s$, which represents the global structural information of said path. 

Simultaneously, the textual information of the reasoning path is retrieved by separately applying a Fusion function to the head, tail and relation embeddings of the path. This results in the textual vectors $z^h$, $z^t$ and $z^s$. Using a concatenation operation, these vectors are subsequently combined into a single vector $z^t$, encapsulating the textual information of the entire reasoning path. 

The core of this stage is the Knowledge Encoder, which now integrates the structural information $z^s$ and the textual information $z^t$ into a combined representation $z^f$. This allows each reasoning path to be encoded into a single token, significantly enhancing efficiency of the LLM by drastically reducing the number of required tokens. Because the fused vector contains both structural and textual information, it enables the model to comprehend the complex interactions within the KG more accurately. Finally, a trainable projector maps the encoded tokens of all reasoning paths into the specific token embedding space of the target LLM, resulting in the knowledge soft prompt $p_s$, which is comprehensible to the LLM.  Remarkably, this process is conducted by tuning solely the parameters of the Knowledge Adapter and Projector,

\subsection{Knowledge Prompts Mixed Reasoning}
Following comes the Prompt-Engineering section of LightPROF, which utilizes the previously prepared tokens, leading the LLM to benefit from the injected knowledge as much as possible, thus answering questions more accurately. For this reason, a mixed prompt strategy is employed, involving a combination of textual templates, so called hard prompts, and the previously generated soft prompts, which are injected into specific areas of the hard prompt. The hard prompt itself includes instructions as well as the question, and the combined input is subsequently arranged in a chat format to serve the LLM. The parameters of the LLM are frozen during this process, to prevent the the possibility of knowledge loss, that can be caused by retraining of an LLMs knowledge base. This effective injection of external knowledge allows the LLM to perform independent and accurate reasoning based on the provided external knowledge. The training objective focuses on maximizing the likelihood of generating a correct answer on questions from a given dataset, given the combined hard and soft prompts\cite{b8}.

\section{Paths-over-Graph}
Another recent framework that will be examined here is Paths-over-Graph (PoG), which introduces a methodology designed to enhance Large Language Model (LLM) reasoning by, similar to LightPROF,focusing on retrieving and processing interconnected reasoning paths that logically link topic entities. This method specifically targets the difficulties associated with multi-hop reasoning, multi-entity questions, and the under-utilization of graph structural information. The architecture of PoG is composed of four distinct, sequential phases: Initialization, Exploration, Path Pruning, and Question Answering.

\subsection{Initialization}
The process commences with the Initialization phase, which establishes the necessary foundation for efficient graph exploration through two key sub-processes: Question Subgraph Detection and Question Analysis. Initially, the framework identifies topic entities within the user's input question and aligns them with corresponding entities in the Knowledge Graph (KG) utilizing BERT-based similarity matching. Subsequently, a "question subgraph" (Gq) is constructed by expanding these topic entities to include their neighbors up to a user-defined maximum depth (Dmax). This subgraph encapsulates all potentially relevant entities and relations. To manage the computational costs and potential noise inherent in large KGs, this subgraph is immediately pruned. Techniques such as node and relation clustering are employed to compress the graph by aggregating similar elements into supernodes. Furthermore, a graph reduction technique using bidirectional BFS is applied to identify and retain only those paths that successfully connect the topic entities, effectively discarding irrelevant branches and unconnected nodes.

Simultaneously, the Question Analysis phase leverages the capabilities of the LLM to decompose the complex input question into simpler, manageable sub-questions. This decomposition not only guides the subsequent reasoning process but also serves to mitigate hallucination by focusing the model's attention. Crucially, the LLM generates a "thinking indicator", a strategic plan that outlines the sequence of entities and predicts the likely depth of the answer (Dpredict) within the graph structure. This predictive capability allows the subsequent exploration phase to begin at an intelligent, estimated depth rather than searching blindly from scratch, thereby optimizing search efficiency.

\subsection{Exploration}
Following initialization, in the Exploration phase the pruned subgraph Gq is actively traversed to discover faithful reasoning paths. This process is executed through three dynamic, hierarchical stages to ensure comprehensive coverage:

1. Topic Entity Path Exploration: Guided by the LLM's thinking indicator, the system prioritizes searching for paths that connect all identified topic entities in the sequence suggested by the model. The search initiates at the predicted depth (Dpredic) and incrementally increases towards the maximum depth (Dmax) only if necessary. This strategy focuses computational resources on the most logically probable connections first.
    
2. LLM Supplement Path Exploration: Acknowledging that KGs may be incomplete or lack specific connections, this stage utilizes the LLM's internal parametric knowledge. The model is prompted to predict potentially missing entities or logical connections based on the current context. These predicted entities are then verified against the KG; if valid, they are incorporated into the exploration pool to uncover supplementary paths that rigid graph traversal might miss.
    
3. Node Expand Exploration: Should the initial stages fail to yield sufficient evidence, the system expands the search space by exploring the neighbors of currently unvisited entities. Unlike methods that treat entities and relations as separate search targets, PoG explores them simultaneously to maintain semantic coherence. New triples are merged into existing paths, and the search iterates until a valid path is identified or the maximum depth limit is reached.

\subsection{Path Pruning} 
Given the sheer scale of KGs, the exploration phase can generate a substantial number of candidate paths. To strictly filter these candidates and ensure relevance, PoG employs a three-step beam search strategy during the Path Pruning phase. The process begins with Fuzzy Selection, a rapid filtering step that uses a pre-trained language model (e.g. SentenceBERT) to compute the semantic similarity between the reasoning paths and the LLM's thinking indicator. The top paths (W1) with the highest similarity scores are retained for further analysis. These survivors then undergo Precise Path Selection, where the LLM itself evaluates the paths, scoring and selecting the top few (Wmax) that are most likely to contain the correct answer. Finally, Branch Reduced Selection is integrated to optimize efficiency for long natural language paths. This method analyzes paths step-by-step (hop-by-hop), pruning branches that diverge from the query's intent early in the sequence. This structural pruning significantly reduces the token load on the LLM by discarding irrelevant path segments before they require full evaluation.

\subsection{Question Answering}
The final phase involves synthesizing the answer from the refined set of reasoning paths. To prevent the LLM from being overwhelmed by raw graph data, a Path Summarizing step first prompts the model to condense the retrieved paths into concise, relevant facts. Subsequently, the LLM evaluates whether these summarized paths provide sufficient evidence to answer both the split sub-questions and the main question. If the evidence is deemed sufficient, the model generates the final response, explicitly citing the specific path used as the reasoning basis. This ensures the output is not only accurate but also interpretable, allowing the user to trace the logic back to specific KG entries. If the evidence is insufficient, the system loops back to the exploration phase to search for deeper or alternative paths, continuing the cycle until a satisfactory answer is found or resources are exhausted\cite{b5}.

\section{Comparative Discussion}
Comparing the two aforementioned frameworks, one can notice that the authors of both in part identified the same challenges, regarding the integration of KGs into LLMs, and utilized similar measurements to deal with them. Accordingly, LightPROF and PoG both recognize the problem of previous frameworks usually exploring the different topic entities independent from one another, and counteract this, by retrieving and processing connected reasoning paths or subgraphs that explicitly link these entities together, thereby preserving the structural dependencies and multi-hop relationships that isolated retrieval might miss. Similarly, both acknowledge that previous works often times translated KGs into a textual format, that wasn't properly conceivable in its entirety by the LLM. However, LightPROF and PoG engage this difficulty in a fundamentally different manner. 

LightPROFs approach is to convert the semantic and structural information of the knowledge graph from a textual format into the embedding space of the LLM, making it as directly interpretable as possible and greatly reducing the share of redundant information. This also has the benefit of reducing the token count drastically, by up to 98\% according to the conducted experiments, leading to LightPROF excelling in efficiency. This in addition to the fact, that in the LightPROF model only the so called knowledge-adapter needs to be trained, in consequence means, that this framework has a tremendous benefit for small-scale LLMs and resource-constrained environments, where efficiency and a low operating cost are required. For the same reason however, LightPROF depends on open-source models that allow access to the embedding space, excluding closed-source models in advance \cite{b8}. 

PoG follows an entirely different approach, effectively keeping a plain-text format at all times and applying smart prompt-engineering, to convert the retrieved knowledge into a prompt format, that preserves the structural and semantic information of the KG as much as possible, without transforming it into the embedding space of the LLM. To get there, PoG makes use of the LLM itself for effective pruning and path-selection. This leads to no additional training being required and even yields the possibility of utilizing closed-source models. The trade-off, however, is higher computational cost during the exploration and the need for a much larger context window, meaning that PoG will only excel when used with large-scale LLMs \cite{b5}.

\section{Conclusion}
In conclusion, the integration of Knowledge Graphs into Large Language Models remains a critical avenue for overcoming the inherent limitations of LLMs regarding hallucinations and lack of transparency. The examination of LightPROF and Paths-over-Graph (PoG) highlights two distinct yet complementary philosophies in addressing the challenges of multi-hop reasoning and structural preservation. LightPROF offers a parameter-efficient solution by translating structural knowledge directly into the embedding space, making it a highly effective framework for small-scale, open-source models where resource constraints are a priority \cite{b8}. Conversely, PoG leverages the advanced semantic planning capabilities of large-scale LLMs to navigate and prune graph paths in natural language, offering a robust zero-shot solution compatible with proprietary, closed-source architectures \cite{b5}.

Ultimately, the choice between these frameworks is dictated by the specific operational constraints of an application. LightPROF is the superior candidate for high-efficiency, training-accessible environments, whereas PoG excels in generalized, inference-heavy applications utilizing state-of-the-art proprietary models. Future research in this domain may focus on bridging this gap, potentially exploring hybrid architectures that combine the retrieval efficiency of embedding-based methods with the flexibility of path-based prompting.

\begin{thebibliography}{00}
\bibitem{b1} Pan, S., Luo, L., Wang, Y., Chen, C., Wang, J., \& Wu, X. (2024). Unifying large language models and knowledge graphs: A roadmap. \textit{IEEE Transactions on Knowledge and Data Engineering, 36}(7), 3580–3599. https://doi.org/10.1109/TKDE.2024.3352100

\bibitem{b2} Brown, T. B., Mann, B., Ryder, N., Subbiah, M., Kaplan, J., Dhariwal, P., ... Amodei, D. (2020). Language models are few-shot learners. \textit{Proceedings of the 34th International Conference on Neural Information Processing Systems} (Article 159). Curran Associates. https://proceedings.neurips.cc/paper/2020/hash/
1457c0d6bfcb4967418bfb8ac142f64a-Abstract.html

\bibitem{b3} Wei, J., Wang, X., Schuurmans, D., Bosma, M., Ichter, B., Xia, F., Chi, E. H., Le, Q. V., \& Zhou, D. (2022). Chain-of-thought prompting elicits reasoning in large language models. \textit{Advances in Neural Information Processing Systems, 35}, 24824–24837. Curran Associates. https://proceedings.neurips.cc/paper\_files/paper/2022/hash/
9d5609613524ecf4f15af0f7b31abca4-Abstract-Conference.html

\bibitem{b4} Besta, M., Blach, N., Kubicek, A., Gerstenberger, R., Podstawski, M., Gianinazzi, L., Gajda, J., Lehmann, T., Niewiadomski, H., Nyczyk, P., \& Hoefler, T. (2024). Graph of thoughts: Solving elaborate problems with large language models. \textit{Proceedings of the AAAI Conference on Artificial Intelligence, 38}(16), 17682–17690. https://doi.org/10.1609/aaai.v38i16.29720

\bibitem{b5} Tan, X., Wang, X., Liu, Q., Xu, X., Yuan, X., \& Zhang, W. (2025). Paths-over-Graph: Knowledge Graph Empowered Large Language Model Reasoning. Proceedings of the ACM on Web Conference 2025, 3505–3522. https://doi.org/10.1145/3696410.3714892

\bibitem{b6} Wen, Y., Wang, Z., \& Sun, J. (2024). MindMap: Knowledge graph prompting sparks graph of thoughts in large language models. \textit{Proceedings of the 62nd Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)}, 10370–10388. Association for Computational Linguistics. https://doi.org/10.18653/v1/2024.acl-long.558

\bibitem{b7} Sun, J., Xu, C., Tang, L., Wang, S., Lin, C., Gong, Y., Ni, L. M., Shum, H.-Y., \& Guo, J. (2024). Think-on-graph: Deep and responsible reasoning of large language model on knowledge graph. \textit{The Twelfth International Conference on Learning Representations}. https://openreview.net/forum?id=nnVO1PvbTv

\bibitem{b8} Ao, T., Yu, Y., Wang, Y., Deng, Y., Guo, Z., Pang, L., Wang, P., Chua, T.-S., Zhang, X., \& Cai, Z.
(2025). LightPROF: A Lightweight Reasoning Framework for Large Language Model on
Knowledge Graph. \textit{Proceedings of the AAAI Conference on Artificial Intelligence, 39}(22), 23424-23432. https://doi.org/10.1609/aaai.v39i22.34510
\end{thebibliography}

\end{document}

