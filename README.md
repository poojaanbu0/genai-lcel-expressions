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
```py
import os
import openai
from dotenv import load_dotenv, find_dotenv

# Load environment variables (OpenAI API Key)
_ = load_dotenv(find_dotenv())
openai.api_key = os.environ['OPENAI_API_KEY']

from langchain.prompts import ChatPromptTemplate
from langchain.chat_models import ChatOpenAI
from langchain.schema.output_parser import StrOutputParser
from langchain.embeddings import OpenAIEmbeddings
from langchain.vectorstores import DocArrayInMemorySearch
from langchain.schema.runnable import RunnableMap

# Step 1: Vector Store Creation
# Create a vector store from given texts
vectorstore = DocArrayInMemorySearch.from_texts(
    ["harrison worked at kensho", "bears like to eat honey"],
    embedding=OpenAIEmbeddings()
)

# Convert the vector store into a retriever
retriever = vectorstore.as_retriever()

# Step 2: Prompt Template
template = """Answer the question based only on the following context:
{context}

Question: {question}
"""
prompt = ChatPromptTemplate.from_template(template)

# Step 3: Model Definition
# Define the OpenAI chat model
model = ChatOpenAI(model_name="gpt-3.5-turbo")

# Define an output parser to format the output
output_parser = StrOutputParser()

# Step 4: LCEL Chain Definition
# Define a RunnableMap that processes input to extract context, format the prompt, and generate an answer
chain = RunnableMap({
    "context": lambda x: retriever.get_relevant_documents(x["question"]),
    "question": lambda x: x["question"]
}) | prompt | model | output_parser

# Step 5: Testing the Chain
# Example questions for testing
question_1 = {"question": "where did harrison work?"}
question_2 = {"question": "what do bears like to eat?"}

# Invoke the chain for each question
response_1 = chain.invoke(question_1)
response_2 = chain.invoke(question_2)

# Print the outputs
print(f"Response 1: {response_1}")
print(f"Response 2: {response_2}")

# Step 6: Inputs Handling (Optional, Additional Example)
inputs = RunnableMap({
    "context": lambda x: retriever.get_relevant_documents(x["question"]),
    "question": lambda x: x["question"]
})

# Test with inputs.invoke
response_from_inputs = inputs.invoke({"question": "where did harrison work?"})
print(f"Response from inputs.invoke: {response_from_inputs}")
```

### OUTPUT:

![389221721-6b9e029a-ad53-4035-a0c0-de0ae1148371](https://github.com/user-attachments/assets/d475da9b-0f6e-415d-ad61-fd0da52b6d53)

![389221768-1a81199a-e8f6-403a-9268-a9c6273a05c1](https://github.com/user-attachments/assets/a3d0c202-ee22-4a5e-bdfd-1603f2aec072)

### RESULT:
The LCEL expression was successfully designed and implemented, incorporating two prompt parameters (context and question) and three key components (prompt, model, and output parser).
