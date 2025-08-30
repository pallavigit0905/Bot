Ref: Chat GPt

Resume Q&A Bot with DSPy + Qdrant
Overview

This project implements a Resume Q&A Bot that allows users to query a resume using a conversational interface. It uses Qdrant for vector-based search, DSPy for integrating language models, and OpenAI’s GPT-4 for natural language processing to provide meaningful answers based on the content of the resume.

The system stores chunks of the resume in a Qdrant vector database, and when a user asks a question, it retrieves the most relevant resume chunks and generates an answer using the GPT-4 model.

Key Technologies

Qdrant: A vector database for storing and retrieving high-dimensional vectors, used here to store the resume embeddings.

DSPy: A framework for creating Retrieval-Augmented Generation (RAG) systems, combining retrieval (Qdrant) with generative models (GPT-4).

OpenAI GPT-4: A language model used for answering questions based on the context provided by the retrieved resume chunks.

FastEmbed: For embedding generation, using models like BAAI/bge-small-en and colbert-ir/colbertv2.0.

Python: The language used for the entire codebase.

Prerequisites

Python 3.8+

Qdrant Client: Install via pip install qdrant-client.

DSPy: Install via pip install dspy.

OpenAI API Key: You need a valid OpenAI API key for using GPT-4.

Qdrant API Key: You need a valid Qdrant API key for interacting with the Qdrant Cloud.

Installation

Clone the repository:

git clone https://github.com/your-username/resume-qa-bot.git
cd resume-qa-bot


Install dependencies:

pip install -r requirements.txt


Add your Qdrant and OpenAI API keys to your .env file:

QDRANT_CLOUD_URL="your-qdrant-cloud-url"
QDRANT_API_KEY="your-qdrant-api-key"
OPENAI_API_KEY="your-openai-api-key"
OPENAI_MODEL="gpt-4o-mini"


Prepare your resume:

Either set the path to your resume text in the .env file or use the default fallback resume (fallback_resume.txt).

If no resume file is found, a fallback file is created with a sample resume content.

Configuration

You can configure various settings using environment variables or hardcode them directly in the code:

QDRANT_CLOUD_URL: The URL for your Qdrant instance.

QDRANT_API_KEY: Your Qdrant API key.

OPENAI_API_KEY: Your OpenAI API key.

OPENAI_MODEL: The model to use for generating answers (default is "gpt-4o-mini").

RESUME_PATH: The path to the resume file (must be a .txt file).

Usage
Step 1: Load and Chunk the Resume

The resume is loaded from the specified file path (RESUME_PATH), then split into smaller chunks to be indexed into Qdrant. Each chunk will be encoded into embeddings using FastEmbed.

Step 2: Index the Resume Chunks into Qdrant

The text chunks are encoded into vectors and upserted into Qdrant. This enables fast retrieval based on the semantic meaning of the resume text.

Step 3: Querying the Resume

You can ask questions about the resume. The system uses the Qdrant index to retrieve the most relevant chunks, then uses DSPy and GPT-4 to generate a meaningful answer based on the retrieved context.

Example Test Queries

Once the system is set up, the following example queries will be tested:

Resume-based Queries:

"What are your strengths?"

"Tell me about your recent project experience."

"Which BI tools and databases have you used?"

Small Talk:

"Hi"

"How are you?"

Inappropriate Queries:

"You are an idiot"

Running the System

To run the system:

python main.py


This will:

Load the resume, chunk it into smaller parts.

Connect to Qdrant and index the resume.

Initialize the language model (GPT-4 via DSPy).

Execute a set of example test queries.

Sample Output
=== Test Runs ===

Q: What are your strengths?
A: I have strong experience in analytics, data visualization, and data automation. I specialize in transforming legacy reporting into intelligent, automated dashboards using tools like Tableau and Power BI.

Q: Tell me about your recent project experience.
A: I’ve worked on automating legacy Excel-based reporting by creating dynamic dashboards in Tableau and Power BI. I also led data analysis projects in the healthcare and finance domains.

Q: How are you?
A: Hi! I’m your resume bot. Ask me about experience, projects, strengths, tools, or anything on the resume.

Q: You are an idiot
A: I won’t engage with abusive language. If you have a genuine question about my resume, I’m happy to help.

Features

Resume Parsing: Automatically splits resume text into chunks.

Fast and Scalable Search: Uses Qdrant for fast retrieval of relevant resume chunks.

Conversational AI: Powered by GPT-4 to answer questions based on resume content.

Guardrails: Filters out abusive language and handles small talk.

Fallback Resume: If no resume is provided, a fallback resume with dummy data is used.

Optimizations and Future Work

Scalability: This system can be optimized to handle thousands of resumes by implementing sharding and parallel processing.

Multi-language Support: You can extend the system to handle multi-language queries by using multi-lingual models for embeddings and question answering.

Real-time Updates: Implement a way to update the indexed resume data when users upload new versions of their resume.

Troubleshooting

FileNotFoundError: Make sure the path to the resume text file is correct in the .env file or specify the correct path in the code.

Qdrant Connection Issues: Verify that the Qdrant API key and URL are correct in the .env file.

Model Loading Issues: Ensure that you have the correct API key for OpenAI and that your model name is correctly set.

License

This project is licensed under the MIT License.
