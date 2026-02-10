# Hospital-Business-Function-Semantic-Search-and-Execution-Planner

## Summary
This project develops a system for semantically searching hospital business functions and generating an execution plan based on identified dependencies. It leverages natural language processing to understand user queries, a graph-based approach to model function prerequisites, and a Gradio interface for interactive demonstration. The system aims to streamline the identification and sequential execution of complex hospital processes.

## Libraries and Technologies Stack
- **pandas**: Used for data manipulation and storage of hospital functions.
- **sentence-transformers**: Provides the `SentenceTransformer` model ('all-MiniLM-L6-v2') for generating semantic embeddings from text queries and function descriptions.
- **scikit-learn**: Specifically, `cosine_similarity` is used to calculate the semantic similarity between user queries and business functions.
- **networkx**: Essential for creating and manipulating the directed graph that represents the dependencies between different hospital functions. It's used for topological sorting to generate execution plans.
- **matplotlib.pyplot**: Used for visualizing the dependency graph.
- **gradio**: Provides a user-friendly web interface for interacting with the semantic search and execution planning system.

## Process Flow
The project implements an end-to-end process that takes a natural language query and provides a relevant hospital function along with its execution plan:

1.  **Sentence-Transformer Model Loading**: The 'all-MiniLM-L6-v2' model is loaded to generate embeddings for text. This model is crucial for the semantic search capabilities.
2.  **Hospital Functions Definition**: A `pandas.DataFrame` named `funcion_de_negocios` is created, containing various hospital functions, their descriptions, and an ID. This DataFrame also includes a 'dictionary' column populated with relevant keywords for each function, enriching the search context.
3.  **Semantic Search Functionality**: The `semantic_search_function` uses the loaded Sentence-Transformer model to convert the user's query into an embedding. It then calculates the cosine similarity between this query embedding and the pre-computed embeddings of all hospital function descriptions. Functions are sorted by similarity, providing the most relevant results.
4.  **Relevance Threshold**: A `RELEVANCE_THRESHOLD` (set to 0.38) is applied to filter out queries that are not sufficiently related to any of the defined hospital functions, ensuring meaningful results.
5.  **Dependency Graph Creation**: A directed graph (`networkx.DiGraph`) is constructed based on a `function_dependencies` dictionary. This graph visually and logically represents the prerequisites for executing each hospital function. For example, 'Gestión de Citas Médicas' depends on 'Administración de Pacientes'.
6.  **Execution Plan Generation**: For the most relevant function identified by the semantic search, the `generate_execution_plan` function uses `networkx.topological_sort` on a subgraph of relevant nodes (ancestors + target function). This produces an ordered list of functions that must be executed sequentially to fulfill the target function, respecting all dependencies.
7.  **Execution Simulation**: Dummy functions (`dummy_functions_dict`) are created for each hospital business function. The `execute_plan` function then simulates the execution of the generated plan, printing messages to demonstrate the sequential activation and completion of each step.
8.  **Gradio Interface**: A comprehensive Gradio interface allows users to input queries, view the top 3 most relevant functions, see the detailed execution plan for the most relevant function, and observe the simulated execution log.

## Graph
<img width="1570" height="1126" alt="image" src="https://github.com/user-attachments/assets/88e37a6e-5793-4880-a374-cb0f439508ea" />


## Conclusions
This project successfully demonstrates a robust system for interpreting natural language queries related to hospital operations, identifying the most relevant business functions, and automatically generating and simulating their execution plans based on predefined dependencies. This approach offers significant potential for automating process workflows, improving operational efficiency, and assisting staff in understanding complex service delivery paths within a hospital setting. The integration of semantic search with graph-based dependency management provides a powerful tool for intelligent process orchestration.

## Authors and Contact Information
- **Author**: Kevin Sinchi, Rafael Serrano.
- **Email**: ksinchim1@est.ups.edu.ec, rserranom@est.ups.edu.ec
