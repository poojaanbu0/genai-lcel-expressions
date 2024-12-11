## Design and Implementation of LangChain Expression Language (LCEL) Expressions

### AIM:
To design and implement a LangChain Expression Language (LCEL) expression that utilizes at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality by analyzing relevant examples of its application in real-world scenarios.

### PROBLEM STATEMENT:
The primary challenge is to create an LCEL expression that can process user queries efficiently by leveraging multiple components in a structured pipeline. This involves retrieving relevant context, formatting it using a prompt, and generating an accurate response through a language model while ensuring a user-friendly output.

### DESIGN STEPS:

#### STEP 1: Environment Setup and Components Initialization

  Install and configure the necessary libraries, such as LangChain and OpenAI.
  Set up the OpenAI API for embedding generation and language model usage.
  Initialize a vector store to store and retrieve document embeddings for contextual understanding.

#### STEP 2: Define LCEL Components

  Prompt: Create a custom prompt template to structure the input query and relevant context.
  Model: Use OpenAI's GPT-3.5-turbo for processing structured inputs and generating responses.
  Output Parser: Implement an output parser to ensure the model’s responses are formatted appropriately.

#### STEP 3: Build and Evaluate LCEL Expression

  Combine the components into an end-to-end pipeline using LangChain’s RunnableMap.
  Test the LCEL expression with diverse real-world examples to evaluate its functionality and accuracy.

### PROGRAM:

### OUTPUT:

![389221721-6b9e029a-ad53-4035-a0c0-de0ae1148371](https://github.com/user-attachments/assets/d475da9b-0f6e-415d-ad61-fd0da52b6d53)

![389221768-1a81199a-e8f6-403a-9268-a9c6273a05c1](https://github.com/user-attachments/assets/a3d0c202-ee22-4a5e-bdfd-1603f2aec072)

### RESULT:
The LCEL expression was successfully designed and implemented, incorporating two prompt parameters (context and question) and three key components (prompt, model, and output parser).
