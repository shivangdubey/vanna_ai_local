# Implementing Vanna AI on Local
This project implements a local AI assistant using Vanna AI with custom data stored in a SQLite database. The assistant leverages the Ollama and ChromaDB modules from Vanna to interact with the database and respond to user queries. Additionally, the assistant is served via a Flask web app, allowing for a user-friendly interface.

## Features
Data Processing with SQLite: Load custom data (e.g., fraud detection data) into a SQLite database and interact with it through SQL queries.
AI Assistant Integration: Use Vanna's Ollama model and ChromaDB for vector-based retrieval and intelligent responses.
Flask API: Serve the AI assistant through a simple web interface using Flask.

### Connecting Database - 
```
import sqlite3
import pandas as pd

# Load your CSV data
df = pd.read_csv('path/to/your/data.csv')

# Create a SQLite database and load the data
conn = sqlite3.connect('mydatabase.db')
df.to_sql(name="fraudTest", con=conn, if_exists='replace', index=False)
conn.commit()
conn.close()

```
### Training the AI
```
from vanna.ollama import Ollama
from vanna.chromadb import ChromaDB_VectorStore

class MyVanna(ChromaDB_VectorStore, Ollama):
    def __init__(self, config=None):
        ChromaDB_VectorStore.__init__(self, config=config)
        Ollama.__init__(self, config=config)

vn = MyVanna(config={'model': 'llama3.1'})
vn.connect_to_sqlite('mydatabase.db')

```
