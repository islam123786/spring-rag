## This Projects creates a RAG pipeline using:
 1. SpringBoot
 2. Vector Embedding via text-embedding-nomic-embed-text-v2-moe (LM Studio-Local)
 3. Postgres as Vector DB
 4. Spring AI to generate response with GPT-3.5

# Run and Setup Embedding Model:
 1. Open LM Studio and run the embedding model "text-embedding-nomic-embed-text-v2-moe".
 2. Open Postman and run the query to see the vector embedding, set "Content-type" as "application/json" under Headers tab

   <img width="1429" height="862" alt="image" src="https://github.com/user-attachments/assets/53cd98c6-5c42-44c2-8350-c53764bd89ab" />

# Install Postgres with pgvector

 ```
  brew install postgresql@17

  brew services start postgresql@17

  psql postgres

  CREATE DATABASE demo_rag;

  \c demo_rag

  -- Enable required extensions
  CREATE EXTENSION IF NOT EXISTS vector;
  CREATE EXTENSION IF NOT EXISTS hstore;
  CREATE EXTENSION IF NOT EXISTS "uuid-ossp";

  -- Create the table to store our documents and embeddings
  CREATE TABLE IF NOT EXISTS vector_store (
    id uuid DEFAULT uuid_generate_v4() PRIMARY KEY,
    content text,
    metadata json,
    embedding vector(768)
  );

  CREATE INDEX ON vector_store USING HNSW (embedding vector_cosine_ops);
  ```
# Create new Springboot project
1. Add all the below dependencies and options as shown below
  <img width="1528" height="811" alt="image" src="https://github.com/user-attachments/assets/2c5e9346-e941-4f65-8bb1-2303a50beaf4" />

2. Add the below dependecy as well 
  ```
    <dependency>
			  <groupId>io.projectreactor.netty</groupId>
			  <artifactId>reactor-netty-http</artifactId>
		</dependency>
  ```
3. Add all the below files
   1. DocumentLoader
   2. RagController
   3. RagService
   4. pdf/spring-boot-reference.pdf
   5. prompts/rag-prompt.st
   6. application.properties (create the API Key from https://openrouter.ai/api and replace <API_KEY>)

# Run the Project and run the below query from postman

Once the project runs and the below message is visible

<img width="343" height="53" alt="image" src="https://github.com/user-attachments/assets/6e507ce1-e571-4d8c-84d0-a90b01e8b954" />

Run the below Query from postman

<img width="1453" height="788" alt="image" src="https://github.com/user-attachments/assets/1ad0b939-0ddb-45c7-819f-a695c1a85494" />







