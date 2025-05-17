# PDF Assistant 📚

A command-line AI assistant that answers questions based on PDF document content using large language models and vector databases.

## Overview

PDF Assistant is a powerful tool that allows you to chat with your PDF documents. Built using the Phi framework, this application extracts information from PDFs, stores it in a vector database, and provides intelligent responses to your questions based on the document content.

The assistant maintains chat history and can perform context-aware searches through your PDF knowledge base, making it an ideal tool for research, document analysis, and information retrieval.

## Features

- **PDF Knowledge Base**: Load and query information from PDF documents
- **Vector Search**: Utilizes PgVector for efficient semantic search
- **Chat History**: Maintains conversation context between sessions
- **CLI Interface**: Easy-to-use command-line interface with markdown support
- **Session Management**: Continue previous chat sessions or start new ones

## Requirements

- Python 3.7+
- PostgreSQL with pgvector extension
- Groq API key

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/PDF-Assistant.git
   cd PDF-Assistant
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Create a `.env` file with your API key:
   ```
   GROQ_API_KEY=your_groq_api_key_here
   ```

4. Ensure you have PostgreSQL running with pgvector extension:
   ```bash
   # Default configuration uses:
   # - Host: localhost
   # - Port: 5532
   # - Database: ai
   # - User: ai
   # - Password: ai
   ```

## Usage

Run the assistant with:

```bash
python pdf_assistant.py
```

### Command line options:

- `--new`: Start a new chat session (default: continue the most recent session)
- `--user`: Specify a user ID (default: "user")

Example:
```bash
# Start a new session
python pdf_assistant.py --new

# Continue the last session
python pdf_assistant.py

# Start a new session for a specific user
python pdf_assistant.py --new --user alice
```

## How It Works

1. The application loads PDF documents from the provided URLs
2. Content is processed and stored in a PostgreSQL vector database using pgvector
3. When you ask questions, the assistant:
   - Searches the vector database for relevant information
   - Uses the LLM to generate a response based on the retrieved content
   - Maintains conversation history for context-aware responses

## Customization

### Changing PDF Sources

Modify the `urls` parameter in the `PDFUrlKnowledgeBase` initialization:

```python
knowledge_base = PDFUrlKnowledgeBase(
    urls=["https://path/to/your/document.pdf"],
    vector_db=PgVector2(collection="your_collection_name", db_url=db_url)
)
```

### Database Configuration

Adjust the PostgreSQL connection settings by modifying the `db_url` variable:

```python
db_url = "postgresql+psycopg://username:password@host:port/database"
```

## Dependencies

- typer: CLI interface
- phi: AI assistant framework
- pgvector: Vector similarity search in PostgreSQL
- dotenv: Environment variable management

## Troubleshooting

- **Database Connection Issues**: Ensure PostgreSQL is running and pgvector extension is installed
- **API Key Errors**: Verify your GROQ API key is correctly set in the .env file
- **PDF Loading Problems**: Check if the PDF URLs are accessible and valid
